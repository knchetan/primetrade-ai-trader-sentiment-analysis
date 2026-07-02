# Primetrade.ai AI Internship Task - Trader Performance vs Market Sentiment

Candidate: K N Chetan  
Role: Artificial Intelligence (AI) Internship  
Dataset: Bitcoin Fear & Greed Index + Hyperliquid historical trader fills

## Objective

Explore the relationship between trader performance and Bitcoin market sentiment, identify hidden behavioral/performance patterns, and convert the findings into practical trading strategy insights.

## Project structure

```text
primetrade_ai_submission/
├── Primetrade_AI_Internship_Task_KN_Chetan.ipynb
├── Primetrade_AI_Report_KN_Chetan.pdf
├── Primetrade_AI_README.md
├── tables/
│   ├── sentiment_scorecard.csv
│   ├── direction_sentiment_scorecard.csv
│   ├── account_sentiment_scorecard.csv
│   ├── coin_sentiment_scorecard.csv
│   ├── daily_performance.csv
│   ├── statistical_tests.csv
│   └── model_metrics.csv
└── charts/
    └── 9 supporting PNG visualizations
```

## Key data handling decisions

1. `Timestamp IST` was parsed as day-first format and merged with daily Fear & Greed data by calendar date.
2. One Fear & Greed date inside the trading range was absent in the raw sentiment file. A continuous daily sentiment calendar was created, and missing sentiment values were forward-filled. This affected only 1 calendar date(s).
3. `Closed PnL = 0` rows were treated as activity/fill rows, not realized outcome rows. Win-rate and average realized PnL were calculated only on rows where `Closed PnL != 0`.
4. Net PnL was calculated as `Closed PnL - Fee`.
5. Because trade PnL is heavy-tailed, the report uses both absolute PnL and capital-efficiency metrics such as `PnL per $1k notional`.

## Headline findings

- Total rows analyzed: 211,224
- Realized PnL rows: 104,408
- Accounts: 32
- Coins: 246
- Trading date range: 2023-05-01 to 2025-05-01
- Total gross PnL: $10,296,959
- Total fees: $245,858
- Total net PnL: $10,051,101
- Overall realized win-rate: 82.30%
- Overall profit factor: 4.42

## Strategic interpretation

- Extreme Greed produced the strongest capital efficiency: $21.60 net PnL per $1k notional.
- Fear produced the largest absolute net PnL because it had the highest traded notional and many realized trades.
- Greed was profitable overall but had weaker win-rate and lower profit factor than Fear and Extreme Greed.
- Same-day Fear & Greed value had weak standalone predictive power at the daily level. The strongest interpretation is to use sentiment as a risk/regime filter, not as a direct long/short signal.
- Trader-level behavior varied substantially by sentiment regime, suggesting a useful sentiment-aware capital allocation layer.

## How to run

The two raw CSV files are included in the project folder. If running elsewhere, keep these two files in the same directory as the notebook:

- `historical_data.csv`
- `fear_greed_index.csv`

Then run the notebook cells from top to bottom. Outputs will be generated into `tables/` and `charts/`.
 
