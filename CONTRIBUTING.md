# Contributing

Thanks for considering a contribution. A few guidelines to keep the content useful.

## The standard for a good definition

Every definition should answer: **why does this term matter when you're building something?**

A definition that just explains what a thing is ("Quantization is the process of reducing numerical precision") is less useful than one that also explains why you'd care ("which is why a 70B model that needs 140GB in full precision can fit on a single consumer GPU at 4-bit").

If you're writing a definition and it could appear in a Wikipedia article without changes, it probably needs more production context.

## Format

Each entry in `GLOSSARY.md` follows this structure:

```
### Term Name
**Full name:** Long-form name if different from term  
**Category:** One of the categories listed below  

Definition paragraph.

**Related:** Term1, Term2, Term3
```

## Categories

- Core Architecture
- Memory & Compute
- Vectors & Retrieval
- Generation & Sampling
- Training & Alignment
- Evaluation
- Prompting & Context
- Agentic AI

If you think a new category is needed, open an issue to discuss before adding it.

## What we don't want

- Definitions that are technically accurate but practically useless
- Terms that are too niche to appear in a real engineering conversation
- Marketing terms dressed up as technical ones
- Anything that requires a PhD to parse

## Corrections

If something is wrong, open an issue with a source. "I think this is incorrect because [source]" is the ideal format. Pull requests for corrections are welcome and will be merged quickly.

## New terms

Open an issue first with: the term, a one-line definition, and why you think it belongs. This avoids wasted effort if the term is out of scope.