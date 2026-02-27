# Zen4 Coder Pro

Zen4 Coder Pro — 80B MoE professional code generation model. Part of the Zen4 family.

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Overview

Zen4 Coder Pro is an 80B parameter Mixture-of-Experts model optimized for professional code generation, refactoring, and software engineering tasks. It activates 14B parameters per forward pass for efficient inference while maintaining frontier-level code quality.

## Key Features

- **80B total / 14B active** MoE architecture
- **128K context window** for full-repository understanding
- Multi-language: Python, TypeScript, Go, Rust, C/C++, Java, and 50+ languages
- Strong performance on code completion, generation, repair, and explanation
- Tool-use and agentic coding capabilities

## Quickstart

```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model_id = "zenlm/zen4-coder-pro"

tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(
    model_id,
    torch_dtype="auto",
    device_map="auto",
)

messages = [
    {"role": "system", "content": "You are Zen, an expert software engineer."},
    {"role": "user", "content": "Write a concurrent rate limiter in Go using token buckets."},
]

inputs = tokenizer.apply_chat_template(messages, return_tensors="pt").to(model.device)
outputs = model.generate(inputs, max_new_tokens=2048)
print(tokenizer.decode(outputs[0][inputs.shape[-1]:], skip_special_tokens=True))
```

## GGUF Quantized

Quantized GGUF models for local inference with llama.cpp:

- [zen4-coder-pro-Q4_K_M.gguf](https://huggingface.co/zenlm/zen4-coder-pro/resolve/main/zen4-coder-pro-Q4_K_M.gguf)
- [zen4-coder-pro-Q8_0.gguf](https://huggingface.co/zenlm/zen4-coder-pro/resolve/main/zen4-coder-pro-Q8_0.gguf)

## Zen4 Family

| Model | Parameters | Focus |
|-------|-----------|-------|
| **Zen4 Ultra** | 405B dense | Frontier general |
| **Zen4 Coder Pro** | 80B MoE | Professional coding |
| Zen4 Coder | 32B | Code generation |
| Zen4 | 32B | General purpose |
| Zen4 Mini | 8B | Efficient deployment |

## Related

- [zen4-ultra](https://github.com/zenlm/zen4-ultra) — Frontier-scale model
- [llama.cpp](https://github.com/zenlm/llama.cpp) — Optimized GGUF inference
- [Zen LM](https://github.com/zenlm) — Full model family

Apache 2.0 · [Zen LM](https://zenlm.org) · [Hanzo AI](https://hanzo.ai)
