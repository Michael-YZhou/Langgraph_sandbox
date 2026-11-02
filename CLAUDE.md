# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A personal sandbox for learning LangGraph (LangChain 1.x). There is no application code yet — expect standalone scripts and Jupyter notebooks to be added over time. Comments in `requirements_full.txt` are in Chinese.

## Environment

- Python lives in the conda env `langchain1.2` (Python 3.13) at `~/miniconda3/envs/langchain1.2`. There is no project-local venv. Use `conda activate langchain1.2`, or call `~/miniconda3/envs/langchain1.2/bin/python` directly.
- Dependencies are pinned in `requirements_full.txt` and are already installed in that env. To check a change before installing it: `pip install --dry-run -r requirements_full.txt`, then `pip check`.
- `langgraph-cli[inmem]` pins `protobuf<7` and `grpcio` to 1.80.x. Don't upgrade either one past those limits, or `langgraph dev` breaks.
- `torch` is deliberately left out. Install it separately (with the right CUDA/MPS build) only if a local model or `unstructured-inference` hi-res parsing needs it.

## Secrets

API keys go in `.env`, which is gitignored. `.env.example` is the committed template and documents the exact variable names each integration reads, such as `HUNYUAN_*` for ChatHunyuan and `TENCENTCLOUD_*` for the Tencent Cloud SDK. Load keys with `python-dotenv`. When you add a new integration that needs a key, add the key to `.env.example` too.

The database variables (`POSTGRES_URI`, `MILVUS_URI`, `MILVUS_TOKEN`) are project conventions rather than names the libraries read. Code has to read them and pass them in explicitly, for example to `PostgresSaver.from_conn_string(os.environ["POSTGRES_URI"])`.

## Commands

- Run the tests: `pytest`. Run a single test: `pytest path/to/test_file.py::test_name`.
- Start the local LangGraph Agent Server with Studio and hot reload: `langgraph dev`. This needs a `langgraph.json` in the repo root (one doesn't exist yet). Set `"env": ".env"` in it so the server loads the keys.
- Start notebooks: `jupyter lab` or `jupyter notebook`.

No linter or formatter is set up.

## Repo notes

- Shared PyCharm project files in `.idea/` are committed. Per-user IDE state is gitignored.
- The remote is `origin` → `git@github.com:Michael-YZhou/Langgraph_sandbox.git`, and the main branch is `main`.
