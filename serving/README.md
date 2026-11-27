# Serving

The Hugging Face repository holds only the LoRA adapter, so the base model is needed too.

Python (Unsloth): see the example on the model card.

vLLM (not tested by the team - check it before relying on it):

```bash
vllm serve unsloth/Llama-3.1-8B-Instruct --enable-lora --max-lora-rank 32 \
  --lora-modules triage=Haziqzul/Llama-3.1-8B-triage-Anti-Hallucinate
```

Use the system prompt in `data/system_prompt.txt` and temperature 0. A GGUF file for Ollama
goes in a separate Hugging Face repository; add its Modelfile here if you make one.
