# Data notes

| Source | Rows | Notes |
|---|---|---|
| Class data | 549 | Provided by the course. Customer messages with category, urgency and needs_human labels. |
| Team-written rows | about 1,430 (in v14) | Written by the team with help from an AI assistant, following the labelling rules in the class data. Covers delivery, refunds, faults, billing, account problems, general questions, Malay and Manglish messages, sarcasm, hidden instructions, messages with several issues, and long natural messages. |

- All rows are synthetic or class-provided. No real personal information.
- About 20% of messages are Malay or mixed Malay-English.
- Format: chat messages (system, user, assistant). The assistant reply is a JSON string.
- `eval_holdout.jsonl` and `hard_probe.jsonl` were written separately and are not in the training data.
- `train_chat_v14.jsonl` (1,981 rows) is the final training set. `train_chat_v7.jsonl` is the earlier 82% set.
- `triage_test_100_questions.xlsx` holds the 100 class test messages (ID and message, no answers). It was never used for training.
