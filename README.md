# Elasticsearch Demo Data for OpenClaw Tutorial

This repository contains DevTools scripts and OpenClaw workspace configuration for the **SearchClaw** tutorial.

## What's Included

- **DevTools Scripts** (`.txt` files): Kibana Dev Tools commands to set up Elasticsearch indices with sample data
- **OpenClaw Workspace**: Agent configuration and environment template

## Repository Structure

```
elasticsearch-openclaw-start-blog/
├── devtools_fresh_produce.txt         ← Creates fresh_produce index (10 products)
├── devtools_app_logs_synthetic.txt    ← Creates app-logs-synthetic index (30 logs)
└── openclaw-workspace-elastic-blog/
    ├── AGENTS.md                      ← Agent briefing
    ├── .env.example                   ← Credentials template
    └── .gitignore
```

## Quick Start

### 1. Set Up Elasticsearch

```bash
curl -fsSL https://elastic.co/start-local | sh
```

### 2. Run DevTools Scripts

1. Open Kibana Dev Tools: http://localhost:5601 → Dev Tools
2. Copy contents of `devtools_fresh_produce.txt`
3. Paste into Dev Tools console
4. Run each numbered block sequentially (Ctrl/Cmd+Enter)
5. Repeat for `devtools_app_logs_synthetic.txt`

### 3. Install the Skill

The `elasticsearch-openclaw` skill is published on ClawHub:

```bash
clawhub install elasticsearch-openclaw
```

Or install globally from ClawHub:

```bash
openclaw skills install elasticsearch-openclaw
```

### 4. Configure OpenClaw

```bash
cp openclaw-workspace-elastic-blog/.env.example openclaw-workspace-elastic-blog/.env
# Edit .env with your Elasticsearch URL and read-only API key
```

### 5. Create the Agent

```bash
openclaw agents add elasticsearch-agent \
  --workspace ~/path/to/elasticsearch-openclaw-start-blog/openclaw-workspace-elastic-blog \
  --non-interactive

openclaw gateway restart
```

## What Gets Created

### fresh_produce Index
- 10 sample products with semantic search
- Uses Jina v5 embeddings via Elastic Inference Service
- Demonstrates: semantic search, hybrid search (BM25 + kNN)

### app-logs-synthetic Index
- 30 synthetic log entries across 4 services
- Classic field types (no semantic_text)
- Demonstrates: aggregations, filtering, observability queries

## Read-Only Design

The `elasticsearch-openclaw` skill is read-only by design:
- ✅ Can search, filter, aggregate
- ❌ Cannot write, update, or delete

This is why the setup must be done manually via DevTools scripts.

## Related Links

- **Tutorial Blog Post**: [SearchClaw: Bring Elasticsearch to OpenClaw](https://elastic.co/blog)
- **Skill on ClawHub**: [elasticsearch-openclaw](https://clawhub.com/skills/elasticsearch-openclaw)
- **OpenClaw Docs**: https://docs.openclaw.ai

## License

Apache 2.0
