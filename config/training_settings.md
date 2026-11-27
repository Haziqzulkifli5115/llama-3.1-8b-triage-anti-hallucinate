# Training settings

Unsloth Studio, LoRA 16-bit, one NVIDIA L4 (22 GB).

| Setting | Best run (v7, 82%) | Published run (v13) |
|---|---|---|
| Base model | unsloth/Llama-3.1-8B-Instruct | unsloth/Llama-3.1-8B-Instruct |
| Training data | train_chat_v7.jsonl (1,651 rows) | train_chat_v14.jsonl (1,981 rows) |
| Method | LoRA, 16-bit | LoRA, 16-bit |
| Rank / alpha / dropout | 32 / 32 / 0.00 | 32 / 32 / 0 |
| Target modules | all-linear | all 7 (all-linear) |
| Epochs | 3 | 3 |
| Learning rate | 1e-4 | 0.0001 |
| Optimizer / scheduler | AdamW 8-bit / linear | AdamW 8-bit / - |
| Batch size x grad accumulation | 2 x 4 | 2 x 4 |
| Context length | 1024 | 1024 |
| Warmup / weight decay | - | 30 steps / - |
| Train on assistant completions only | yes | yes |
| Packing | off | off |
| Seed | 3407 (also 2025) | 3407 |
