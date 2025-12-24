# JSON x TOON Applications

Production-ready applications and utilities for mixing JSON with TOON format for optimized data structures.

## Overview

This repository contains practical, real-world applications of the JSON/TOON mixed encoding pattern. TOON is a tabular-compact representation format that's more efficient than JSON for large arrays of uniform objects.

## Design Philosophy

- **Hybrid Approach**: Keep complex configs in JSON, encode large tabular data as TOON
- **Auto-Detection**: Automatically identify arrays eligible for TOON encoding
- **Cost Savings**: Reduce API costs, latency, and token consumption
- **Framework Agnostic**: Works with any LLM, framework, or data pipeline

## Documentation

### 📚 Core Resources

- **[applications.md](./applications.md)** - 10 real-world use cases with ROI calculations
  - LangChain memory optimization
  - Incident response analysis
  - SQL result caching
  - Real-time bidding systems
  - E-commerce dashboards
  - And more...

- **[Conversation Reference](https://claude.ai/share/8b6217db-7f84-4167-8326-3ccd914286be)** - Original design discussion and architecture decisions

## Quick Wins

### 1. LangChain Memory Compression

```python
# Save 46K tokens per request
# Cost savings: $13,800/month (100K requests)
# Faster responses, better UX
```

### 2. Analytics Dashboard

```python
# Load 2000-row tables in 180ms instead of 2000ms
# Mobile users will thank you
```

### 3. SQL Cache Layer

```python
# Cut Redis costs by $140/month
# 67% smaller cache payloads
```

## Key Metrics

| Use Case | Token Savings | Cost Savings | Latency Improvement |
|----------|---------------|--------------|---------------------|
| LangChain Memory | 46K/request | $13,800/mo | N/A |
| Incident Analysis | 10K lines | N/A | -15 min MTTR |
| SQL Caching | 67% reduction | $140/mo | N/A |
| Real-Time Bidding | N/A | N/A | -15ms per bid |
| E-commerce Tables | N/A | N/A | 91% faster load |

## When to Use TOON

✅ **Good Use Cases:**
- Arrays with 10+ uniform objects
- Mostly primitive values (strings, numbers, booleans)
- Large datasets read by models multiple times
- Time-series data, logs, metrics

❌ **Poor Use Cases:**
- Small arrays (<10 items)
- Highly nested objects
- Mixed/heterogeneous schemas
- Binary or complex data structures

## Integration Patterns

### Agent Frameworks
```
Config: JSON
Tool outputs: TOON
Memory window: TOON encoded
```

### RAG Systems
```
Query/filters: JSON
Documents/tables: TOON
```

### Evaluation Pipelines
```
Scenario config: JSON
Results/metrics: TOON
```

## Getting Started

1. Read [applications.md](./applications.md) for concrete examples
2. Review the [conversation](https://claude.ai/share/8b6217db-7f84-4167-8326-3ccd914286be) for design details
3. Implement auto-detection in your framework
4. Measure cost savings and latency improvements

## ROI Calculator Example

**100K requests/month with 500-row arrays:**
- Token savings: 46K per request
- Monthly token savings: 4.6B tokens
- Cost reduction: $13,800/month (at typical pricing)
- Plus: Faster responses, better UX, lower infrastructure costs

## References

- **Original Discussion**: https://claude.ai/share/8b6217db-7f84-4167-8326-3ccd914286be
- **TOON Format**: [See applications.md for format details](./applications.md)
- **TypeScript Utilities**: Coming soon

## Contributing

Contributions welcome! Areas for expansion:
- TypeScript/JavaScript implementations
- Framework-specific integrations (LangChain, Vercel AI, etc.)
- Benchmarking and performance comparisons
- Additional use case examples

## License

MIT
