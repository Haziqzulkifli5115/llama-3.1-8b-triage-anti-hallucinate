# Experiment log

Scores are from the course leaderboard.

| Run | Data | Change | Score | Category | Urgency | Recall | JSON | Hard |
|---|---|---|---|---|---|---|---|---|
| Baseline | none | Llama 3.1 8B, not fine-tuned | 31% | 84 | 40 | 95 | 99 | 30 |
| v6 | 1,560 rows | class data plus first additions | 77% | | | | | |
| v7 seed 3407 | 1,651 | v6 plus 91 long natural messages | 82% | 93 | 94 | 95 | 100 | 80 |
| v7 seed 2025 | 1,651 | different seed | 82% | | | | | |
| v8 | 1,738 | v7 plus 87 targeted rows | 78% | 95 | 90 | 85 | 100 | 76 |
| v9a | 1,707 | v7 plus 56 escalation rows | 80% | | | | | |
| v10 | 2,200 | v7 plus class data counted twice | 79% | | | | | |
| v13 (published) | 1,981 | final data (v14) | 84% | | | | | |

What we learned:
- v7 gave the same score on two seeds, so 82% was not a lucky run.
- Adding "harmless but scary-sounding" examples (v8) lowered Recall from 95% to 85%.
- Counting the original class data twice (v10) did not help.

The baseline row comes from `triage_baseline_scorecard.xlsx` (Ollama `llama3.1:latest`, 4-bit, temperature 0). Its Recall is needs_human recall; its JSON column is valid JSON in the right shape.
