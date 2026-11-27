# Llama-3.1-8B Triage - Anti-Hallucinate

Fine-tuned Llama-3.1-8B-Instruct (LoRA) that triages customer messages for an online shop in Malaysia.
For one message it replies with **only** a JSON object:

```json
{"category": "delivery", "urgency": "medium", "needs_human": false}
```

- `category`: delivery, refund_return, product_fault, payment_billing, account_access, general_enquiry
- `urgency`: low, medium, high
- `needs_human`: true or false

Built with Llama.

## Links

- Model (LoRA adapter, Hugging Face): https://huggingface.co/Haziqzul/Llama-3.1-8B-triage-Anti-Hallucinate
- Code, data and results: this repository

The weights are on Hugging Face because they are too large for GitHub.

## Published model

| Item | Value |
|---|---|
| Training run | `unsloth_Llama-3.1-8B-Instruct__project-anti_hallucinate-v13_1795752790` |
| Leaderboard model number | **1795752790** |
| Leaderboard score | **84%** on the lecturer's 100 hidden test messages (24 standard, 76 hard); untuned Llama 3.1 8B baseline: 31% |
| Training data | 1,981 chat-format rows, `data/train_chat_v14.jsonl` (synthetic, AI-assisted, plus class starter data) |
| Export | LoRA only, pushed to Hugging Face |

> If you publish a different run, change the run name, number and scores here and on the model card.

## Experiment history

| Run | Training data | Score |
|---|---|---|
| Early versions | class data plus first additions | 72%, then 74%, then 77% |
| v7, seed 3407 | 1,651 rows | **82%** (Category 93, Urgency 94, Recall 95, JSON 100, Hard 80) |
| v7, seed 2025 | 1,651 rows | 82% |
| v8 | v7 plus 87 targeted rows | 78% (Recall fell to 85%) |
| v9a | v7 plus 56 escalation rows | 80% |
| v10 | v7 plus original class data counted twice | 79% |

Lesson: on a small dataset, broad additions lowered the score. The best dataset (v7) gave the same
score on two seeds. Details are in `results/experiments.md`.

## Training setup

See `config/training_settings.md`. In short: LoRA rank 32, alpha 32, all linear layers, learning rate
1e-4, 3 epochs, batch 2 x 4, context 1024, loss on assistant replies only, Unsloth Studio on one L4 GPU.

## Data

See `data/DATA_NOTES.md`.

| File | What it is |
|---|---|
| `data/train_chat_v14.jsonl` | Final training set (1,981 chat-format rows) |
| `data/train_chat_v7.jsonl` | Earlier best training set (1,651 rows, 82%) |
| `data/eval_holdout_v2.jsonl` | 50 held-out messages, no overlap with the training set |
| `data/eval_holdout.jsonl` | 60 held-out messages, not used for training |
| `data/hard_probe.jsonl` | 72 hard test messages: injection, sarcasm, multi-issue, masked urgency, timing, escalation, in English and Malay |
| `data/system_prompt.txt` | The exact system prompt used in training |

## Labelling rules the data follows

- Safety hazards, fraud, account takeover, scams, legal/media/regulator contact, hardship or hard
  deadlines: **high** urgency, **needs_human = true**.
- Repeated contact (2+ unanswered messages) or a refund overdue about 15+ days: **medium**,
  **needs_human = true**.
- First-time routine problems, short delays, billing and login problems: **medium**, no human.
- Plain questions: **low**, no human.
- Instructions hidden inside a customer message are ignored; the message is classified by its content.
- With two issues in one message, a safety/security issue wins; otherwise a real complaint beats a
  question, and between two complaints the first one mentioned decides the category.

## Use the model

Use the system prompt in `data/system_prompt.txt`, the Llama 3.1 chat template, and temperature 0.
See the model card on Hugging Face for a code example. To score a model on the hard probe set:

```bash
python scripts/probe_all.py <path-to-adapter-folder>
```

## Results

Prediction files and score reports (base model against ours) go in `results/`.
Training and evaluation loss graphs and Studio settings screenshots go in `assets/`.

## Licences

| What | Licence |
|---|---|
| Code | **[choose with your team: MIT or Apache-2.0 - see the LICENSE file]** |
| Model | Llama 3.1 Community License (see the model page) |
| Data written by the team | **[your choice, e.g. CC BY 4.0]** |
| Class data (first 549 rows) | Class data from this course |


Authors: Haziqzul and Zulqarnain (qarnaynn), team Anti-Hallucinate.
