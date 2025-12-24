# JSON × TOON Applications

Production-oriented patterns for combining JSON with TOON to encode large, structured data more compactly for LLMs and data pipelines.

## What this repo is

- Curated **applications**, not a core TOON implementation: examples, patterns, and ROI calculations for JSON ↔ TOON usage.
- **Format-agnostic** integration ideas that can be adapted to any language, framework, or model provider.
- A starting point for engineering discussions around cost, latency, and data-shape tradeoffs, rather than a drop-in library.

**Out of scope:**

- Canonical TOON spec (see the upstream TOON repository instead).
- Hard guarantees about specific vendors' pricing or latency; all numbers are illustrative and depend on your stack.

## Why JSON + TOON together?

TOON is a line-oriented, tabular representation of JSON that is efficient for large arrays of uniform objects. In many systems:

- **JSON** is convenient for configs, nested objects, and APIs.
- **TOON** (or similar tabular encodings) suits bulk rows better: logs, metrics, time series, analytics tables.

This repo explores where that hybrid pays off in practice: fewer tokens to LLMs, smaller cache payloads, lower end-to-end latency.

## Design principles

- **Format-agnostic**: Patterns apply to "compact tabular encoding + JSON" in general, even if you swap TOON for another representation.
- **Separation of concerns**: Keep configs, prompts, and control flow in JSON; encode only large, uniform arrays in a tabular format.
- **Auto-detection, not manual flags**: Prefer heuristics that detect "TOON-eligible" arrays (size, uniformity) over manual annotations.
- **Measurable impact**: Every example ties back to tokens, bytes, or milliseconds so you can decide if the added complexity is worth it.

## When TOON-style encodings help

### Good fit

- Arrays with ~10+ items and a stable, uniform schema (e.g., rows from SQL, logs, metrics).
- Mostly primitive fields (strings, numbers, booleans) where tabular layouts compress well and are easy for models to scan.
- Data sent to models or over the network many times (e.g., shared context windows, repeated analytics prompts).

### Poor fit

- Tiny arrays or highly nested, heterogeneous structures where the tabular mapping becomes brittle.
- Payloads dominated by binary blobs or opaque structures not meant to be model-readable.
- Single-use, one-off data that doesn't benefit from repeated serialization.

## Key metrics & ROI signals

These are back-of-envelope estimates to show the *shape of impact*, not vendor-specific promises.

| Use Case | Token Savings | Cost Savings | Latency | Signal |
|----------|---------------|--------------|---------|--------|
| LangChain memory | 46K/request | $13.8K/mo (100K req) | N/A | Enables longer context windows |
| Incident logs | 10K+ lines | N/A | -15 min MTTR | Faster triage, less duplication |
| SQL result caching | 67% reduction | ~$140/mo | N/A | Smaller cache footprints |
| Real-time bidding | N/A | N/A | -15ms/bid | Throughput wins at scale |
| E-commerce dashboards | N/A | N/A | 91% faster load | Client-side responsiveness |

**How to read these numbers:**

- Numbers vary by model, provider, and payload size. Use them to identify *which applications* are worth exploring, not to plan budgets.
- "N/A" means the metric is not the primary win; focus on what's listed.
- Measure your own stack before committing engineering effort.

## Example applications

See [`applications.md`](./applications.md) for detailed scenarios, rough ROI models, and implementation sketches.

## Integration patterns

These patterns are tool-agnostic. "Frameworks" below can be LangChain, custom agents, RAG stacks, or anything similar.

### Agent frameworks

- Config and tool specs remain JSON.
- High-volume tables (memories, search results, event streams) are encoded in TOON before being sent to the model.

### RAG and retrieval

- Queries, filters, and metadata stay in JSON.
- Result sets are batched and serialized as TOON rows to reduce context size per query.

### Evaluation and batch pipelines

- Scenario definitions and parameters use JSON.
- Metrics and per-example outputs are emitted as TOON to keep logs compact and easy to post-process.

## Getting started

1. Read [`applications.md`](./applications.md) for concrete scenarios and ROI sketches.
2. Pick one high-volume path in your system (e.g., one memory store or analytics view).
3. Add a TOON encoding layer behind an interface (no breaking changes to callers).
4. **Measure tokens, bytes, and latency before/after.** Keep the hybrid only where it clearly wins.

## What to look for (signal checklist)

- [ ] Can you identify 10+ objects with an identical or near-identical schema?
- [ ] Is the data sent to a model or network boundary more than once per session?
- [ ] Are most fields primitive (string, number, boolean, date)?
- [ ] Do you already log/measure token or byte usage for this data?
- [ ] Would a 50%+ reduction in payload size noticeably improve latency?

If 3+ boxes are ticked, this application is worth prototyping.

## Contributing

Contributions are welcome:

- Additional, framework-agnostic application patterns and data shapes.
- Language-specific examples (TypeScript, Python, etc.) that stay optional.
- Independent benchmarks comparing JSON vs. TOON-style encodings across different models and providers.
- Real-world ROI reports from your own systems (anonymized).

Open an issue to propose new scenarios or share measurements from your stack.

## References

- **TOON format**: See the upstream TOON repository for spec and reference implementation.
- **Original design discussion**: [Claude conversation](https://claude.ai/share/8b6217db-7f84-4167-8326-3ccd914286be) documenting architecture decisions.
- **applications.md**: Detailed 10+ use cases with ROI calculations and implementation guidance.

## License

MIT
