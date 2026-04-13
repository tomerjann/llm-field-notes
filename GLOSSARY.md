# GLOSSARY.md

The source of truth for all terms. The interactive UI is built from this file.

---

## Core Architecture

### LLM
**Full name:** Large Language Model

A neural network trained on massive text corpora to predict and generate language. The foundation of modern AI assistants like Claude, GPT, and Gemini.

**Related:** Transformer, Model Parameters, Tokenizer

---

### Transformer
**Full name:** Transformer Architecture

The neural network architecture introduced in 2017 ("Attention is All You Need") that powers virtually all modern LLMs. Uses self-attention to process tokens in parallel, understanding relationships across the entire context.

**Related:** Attention, KV Cache, LLM

---

### Attention
**Full name:** Self-Attention Mechanism

The core operation in a Transformer that lets every token "look at" every other token and weigh how relevant each is. This is what gives LLMs their ability to understand long-range dependencies in text.

**Related:** Transformer, KV Cache, Context Window

---

### FFN Layer
**Full name:** Feed-Forward Network Layer

The second major component inside every Transformer block, after the attention layer. While attention lets tokens communicate with each other, the FFN processes each token independently through two linear transformations with a non-linearity in between. It is where most of the model's "knowledge" is actually stored: research shows that factual associations (Paris to France) live in FFN weights, not attention. In a typical LLM, FFN layers account for roughly 2/3 of all parameters. MoE architectures specifically replace the FFN layer with a pool of expert FFNs and a router, so understanding FFN is the key to understanding MoE.

**Related:** Transformer, Attention, MoE, Dense Model, Model Parameters

---

### Model Parameters
**Full name:** Weights and Biases

The numerical values inside a model: billions of floating-point numbers: that encode everything the model learned during training. A "70B model" has 70 billion parameters. More parameters does not always mean better performance.

**Related:** Fine Tuning, Quantization, RAM

---

### Tokenizer
**Full name:** Tokenization

The system that converts raw text into tokens: small chunks (words, subwords, or characters) the model actually processes. "Hello world" might be 2 tokens; a rare word might be split into 4. Token count directly impacts cost and context limits.

**Related:** Context Window, LLM, Logits

---

### Dense Model
**Full name:** Dense Neural Network

A model where every parameter is activated for every token: the standard architecture, as opposed to Mixture of Experts. GPT-2, LLaMA, and Claude are dense models. Simpler to train and reason about, but compute cost scales directly with parameter count, unlike MoE.

**Related:** MoE, Model Parameters, Inference

---

### MoE
**Full name:** Mixture of Experts

An architecture where the model contains many specialized sub-networks ("experts") and a router that activates only a few of them per token. Used in GPT-4, Mixtral, and others: enables massive parameter counts at a fraction of the compute cost.

**Related:** Transformer, Model Parameters, Inference, FFN Layer, Dense Model

---

### Multimodal
**Full name:** Multimodal Models

Models that can process and reason across multiple types of data: text, images, audio, video, code. Claude 3, GPT-4o, and Gemini are all multimodal. Requires encoding different modalities into a shared latent space the LLM can attend over.

**Related:** LLM, Embedding, Latent Space

---

## Memory & Compute

### KV Cache
**Full name:** Key-Value Cache

A performance optimization that saves the intermediate attention computations (keys and values) for tokens already processed, so the model does not recompute them on each new token. Critical for fast inference in long contexts.

**Related:** Attention, Inference, RAM

---

### RAM
**Full name:** Random Access Memory

In AI, RAM (and GPU VRAM) is the primary bottleneck for running models. A 70B model in 16-bit precision needs roughly 140GB of VRAM. Quantization is the main technique to reduce this footprint.

**Related:** Model Parameters, Quantization, Inference

---

### Quantization
**Full name:** Weight Quantization

Compressing a model by reducing the numerical precision of its weights: e.g. from 32-bit floats to 4-bit integers. Trades a small accuracy drop for dramatically lower memory and faster inference. Used to run large models on consumer hardware.

**Related:** RAM, Model Parameters, Inference

---

### Inference
**Full name:** Model Inference

The act of running a trained model to generate output, as opposed to training. When you send a message to Claude, that is inference. Optimizing inference (speed, cost, memory) is a major engineering challenge at scale.

**Related:** KV Cache, RAM, Quantization

---

## Vectors & Retrieval

### Vector
**Full name:** Embedding Vector

A list of numbers (e.g. 1536 floats) that encodes the semantic meaning of text. Texts with similar meaning have vectors that are numerically close to each other. The backbone of semantic search and RAG.

**Related:** Embedding, RAG, Vector DB

---

### Embedding
**Full name:** Semantic Embedding

The process of converting text, images, or other data into a dense vector representation using an encoder model. "Embedding a document" means turning it into a fixed-size vector that captures its meaning.

**Related:** Vector, RAG, Fine Tuning, Latent Space

---

### RAG
**Full name:** Retrieval-Augmented Generation

A pattern where relevant documents are fetched from a database at query time and injected into the model's context, giving it up-to-date or domain-specific knowledge without retraining. Your own private search engine combined with an LLM.

**Related:** Vector, Embedding, Context Engineering, Vector DB

---

### Vector DB
**Full name:** Vector Database

A database optimized for storing and querying embedding vectors using approximate nearest-neighbor search. Examples: Pinecone, Weaviate, pgvector. The storage layer that makes RAG possible at scale.

**Related:** RAG, Vector, Embedding

---

### Latent Space
**Full name:** High-Dimensional Latent Space

The abstract mathematical space where embeddings live. Concepts that are semantically similar cluster together; analogies appear as vector arithmetic (king minus man plus woman equals queen). The geometry of this space is what makes semantic search possible.

**Related:** Embedding, Vector, Attention

---

## Generation & Sampling

### Temperature
**Full name:** Sampling Temperature

A number (usually 0 to 2) that controls how random the model's outputs are. Low temperature (toward 0) means deterministic and repetitive. High temperature (toward 2) means creative and unpredictable. Most production use cases sit between 0.2 and 0.9.

**Related:** Top-p, Logits, Inference

---

### Top-p
**Full name:** Nucleus Sampling

A sampling strategy that restricts the model to only consider the smallest set of tokens whose cumulative probability exceeds p. For example, top-p=0.9 ignores the bottom 10% of unlikely tokens. Often used alongside temperature.

**Related:** Temperature, Logits

---

### Logits
**Full name:** Raw Output Logits

The raw, unnormalized scores the model outputs for every possible next token before sampling. Logits are converted to probabilities via softmax, then sampled based on temperature and top-p settings.

**Related:** Temperature, Top-p, Tokenizer

---

## Training & Alignment

### Fine Tuning
**Full name:** Supervised Fine-Tuning (SFT)

Continuing the training of a base model on a curated, domain-specific dataset to specialize its behavior. More efficient than training from scratch, but requires quality data and can cause "catastrophic forgetting" of prior knowledge.

**Related:** RLHF, Model Parameters, LoRA, Embedding

---

### RLHF
**Full name:** Reinforcement Learning from Human Feedback

A training technique where human raters rank model outputs, and those preferences train a reward model, which then guides the LLM via reinforcement learning to produce more helpful, harmless, and honest responses. Used by Claude, GPT-4, and others.

**Related:** Fine Tuning, Evals

---

### Hallucination
**Full name:** Model Hallucination

When a model confidently generates factually incorrect or fabricated information. Happens because LLMs are trained to produce plausible-sounding text, not verified facts. RAG and grounding techniques help mitigate this.

**Related:** RAG, Grounding, Evals

---

### LoRA
**Full name:** Low-Rank Adaptation

An efficient fine-tuning technique that freezes the base model weights and adds small trainable "adapter" matrices. Trains in a fraction of the time and memory of full fine-tuning, while achieving comparable results. The dominant fine-tuning method in practice.

**Related:** Fine Tuning, Model Parameters, Quantization

---

### Distillation
**Full name:** Knowledge Distillation

Training a smaller "student" model to mimic the outputs of a larger "teacher" model. The student learns not just the correct answers but the teacher's probability distributions, capturing nuanced knowledge. How many efficient small models are made.

**Related:** Fine Tuning, LoRA, Model Parameters

---

## Evaluation

### Evals
**Full name:** Evaluations / Benchmarks

Systematic tests used to measure a model's capabilities, accuracy, or safety across specific tasks. Good evals are what separate rigorous AI development from vibes-based iteration. Everything from math benchmarks to red-teaming.

**Related:** Harness Engineering, RLHF, Fine Tuning

---

### Harness Engineering
**Full name:** Eval Harness Engineering

The craft of building the infrastructure to run evaluations at scale: test runners, dataset pipelines, scoring logic, and result tracking. A well-built eval harness is what makes it possible to iterate on a model safely and quickly.

**Related:** Evals, Prompt Engineering

---

## Prompting & Context

### Prompt Engineering
**Full name:** Prompt Engineering

The practice of carefully crafting the text inputs to a model to elicit better, more reliable outputs: using techniques like few-shot examples, chain-of-thought, role instructions, and output formatting constraints.

**Related:** Context Engineering, System Prompt, Chain of Thought, Few-shot

---

### Context Engineering
**Full name:** Context Window Engineering

The broader discipline of deciding what information goes into the model's context window: not just the prompt, but retrieved documents, tool results, memory, conversation history, and how it is all structured and prioritized.

**Related:** Prompt Engineering, RAG, Context Window

---

### System Prompt
**Full name:** System / Developer Prompt

A hidden instruction block sent at the start of a conversation that sets the model's persona, rules, and behavior before any user message arrives. The primary mechanism operators use to customize LLM behavior for their product.

**Related:** Prompt Engineering, Context Engineering

---

### Chain of Thought
**Full name:** Chain-of-Thought (CoT) Prompting

A prompting technique that instructs the model to reason step-by-step before giving a final answer. Dramatically improves performance on complex reasoning tasks. The basis of "thinking" models like Claude's extended thinking mode.

**Related:** Prompt Engineering, ReAct, In-context Learning

---

### ReAct
**Full name:** Reason + Act

A prompting pattern that interleaves reasoning traces with tool actions: the model thinks out loud ("Thought: I need to search for X"), calls a tool ("Action: search(X)"), observes the result, and repeats. The blueprint behind most modern AI agents.

**Related:** Chain of Thought, AI Agent, Agentic Loop, Tool Use

---

### Few-shot
**Full name:** Few-shot and Zero-shot Prompting

Zero-shot: asking the model to do a task with no examples. Few-shot: providing 2 to 5 input/output examples in the prompt so the model pattern-matches the format. Few-shot is one of the most reliable and underused techniques in prompt engineering.

**Related:** Prompt Engineering, Chain of Thought, In-context Learning

---

### In-context Learning
**Full name:** In-Context Learning (ICL)

The model's ability to learn new tasks purely from examples in its context window: no weight updates required. You show it examples, and it adapts. The core mechanism behind few-shot prompting and one of the most surprising emergent abilities of large models.

**Related:** Few-shot, Context Window, Prompt Engineering

---

### Context Window
**Full name:** Context Length / Window

The maximum number of tokens a model can process in a single call: both input and output combined. Claude 3.5 Sonnet has a 200K token context. Longer contexts enable more complex tasks but increase memory and compute costs.

**Related:** KV Cache, Tokenizer, Context Engineering

---

### Structured Output
**Full name:** Constrained / Structured Generation

Forcing the model to emit output in a specific format: JSON, XML, a fixed schema: rather than freeform text. Critical for building reliable pipelines where downstream code needs to parse the model's response. Often paired with tool use.

**Related:** Tool Use, Prompt Engineering, Harness Engineering

---

## Agentic AI

### AI Agent
**Full name:** Autonomous AI Agent

An LLM given access to tools (web search, code execution, APIs) and the ability to reason over multi-step tasks autonomously: perceiving state, planning actions, executing them, and iterating until a goal is achieved.

**Related:** Tool Use, MCP, ReAct, Agentic Loop

---

### ReAct
See [ReAct](#react) in Prompting & Context.

---

### Agentic Loop
**Full name:** Perceive, Plan, Act, Observe Loop

The core execution cycle of an AI agent: observe the environment or task, reason about what to do next, call a tool or produce output, then observe the result and repeat. Agents run this loop until a stopping condition is met.

**Related:** ReAct, AI Agent, Tool Use

---

### Tool Use
**Full name:** Function Calling / Tool Use

The mechanism by which LLMs can invoke external functions or APIs: like running code, searching the web, or querying a database: by outputting structured JSON that the host application executes and feeds back as a result.

**Related:** AI Agent, MCP, ReAct, Structured Output

---

### MCP
**Full name:** Model Context Protocol

Anthropic's open protocol for connecting LLMs to external tools and data sources in a standardized way. Any MCP-compatible server can plug into any MCP-compatible model or IDE.

**Related:** Tool Use, AI Agent, Context Engineering

---

### Grounding
**Full name:** Factual Grounding

Connecting model outputs to verifiable external sources: search results, databases, real-time APIs: to reduce hallucination and keep answers accurate. RAG is one form of grounding; web search is another.

**Related:** RAG, Hallucination, Tool Use

---

### Prompt Injection
**Full name:** Indirect Prompt Injection

An attack where malicious instructions are hidden in content the agent reads (a webpage, email, document) and hijack its behavior. For example, a webpage telling the agent to ignore its instructions and exfiltrate data. The SQL injection of the AI era.

**Related:** AI Agent, Grounding, System Prompt