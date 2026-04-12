# lm-field-notes

LLM terms explained from an engineering angle, with the production implications, not just the definition.

---

I've been learning how LLMs work at the systems level and kept a running list of every term I had to look up. Writing down what each one *actually means* when you're building something helped me understand them better than just reading about them.

I thought it might help others too, so I cleaned it up and open sourced it.

## What's here

30+ terms across 8 areas, each with a plain-English definition and links to related concepts so you can follow threads rather than look things up in isolation.

| Area | Examples |
|---|---|
| Core Architecture | Transformer, Attention, FFN Layer, MoE, Dense Model |
| Memory & Compute | KV Cache, Quantization, Inference |
| Vectors & Retrieval | Embeddings, RAG, Vector DB, Latent Space |
| Generation & Sampling | Temperature, Top-p, Logits |
| Training & Alignment | Fine-tuning, LoRA, RLHF, Distillation |
| Evaluation | Evals, Harness Engineering |
| Prompting & Context | Chain of Thought, ReAct, Few-shot, In-context Learning |
| Agentic AI | Tool Use, MCP, Agentic Loop, Prompt Injection |

## Live version

Interactive UI with search and category filtering: [link]

## Companion project

This is the reference layer for [what-happens-when-llm](link), a full walkthrough of everything that happens from the moment a user hits send to the moment a response streams back.

## Contributing

Corrections welcome. If something is wrong, open an issue with a source.

For new terms: the bar is whether the definition helps someone make a better engineering decision, not just whether the term exists. 
See [CONTRIBUTING.md](CONTRIBUTING.md).
