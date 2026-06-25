# Building Useful AI Agents with Agno + OpenRouter

Hands-on notebooks for the workshop. We build **"Safari"**, a travel-planning assistant,
growing it from a one-liner into a stateful, production-shaped system.

| Notebook | Session | Covers (slides) |
|----------|---------|-----------------|
| [`01_agno_basics.ipynb`](01_agno_basics.ipynb) | **Foundations** | What is Agno · First Agent · Tools · Structured Outputs · Teams (1–10) |
| [`02_agno_advanced.ipynb`](02_agno_advanced.ipynb) | **Advanced** | Memory · Knowledge (RAG) · Storage · Workflows (11–17) |

## Setup

Requires [uv](https://docs.astral.sh/uv/) and Python 3.12+.

```bash
# 1. Install dependencies into a local virtual env
uv sync

# 2. Register the kernel for Jupyter (once)
uv run python -m ipykernel install --user --name agno-workshop

# 3. Add your OpenRouter key
cp .env.example .env        # then edit .env and paste your key

# 4. Launch
uv run jupyter lab          # or: uv run jupyter notebook
```

In the notebook, select the **agno-workshop** kernel (top-right).

## Notes

- **Model gateway:** [OpenRouter](https://openrouter.ai) — one key, hundreds of models.
  The model is set via the `MODEL_ID` variable near the top of each notebook
  (default `openai/gpt-4o-mini`; swap to any cheap model you like).
- **Embeddings (RAG):** OpenRouter doesn't serve embeddings, so the Knowledge section uses
  **FastEmbed**, which runs a small embedding model locally (free, downloads ~70 MB on
  first use). No extra API key needed.
- **Storage:** SQLite (`safari.db`) for zero-setup persistence. Swap `SqliteDb` for
  `PostgresDb` in production with no other code changes.
- **API version:** written for **Agno v2** (`agno.db.sqlite.SqliteDb`, `db=`,
  `output_schema=`). The slides show some older v1 snippets; the notebooks note the
  differences where relevant.

## Reset

To start clean, delete the generated state:

```bash
rm -rf safari.db safari_lancedb/
```
