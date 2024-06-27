<p align="left">
  <a href="https://r2r-docs.sciphi.ai"><img src="https://img.shields.io/badge/docs.sciphi.ai-3F16E4" alt="Docs"></a>
  <a href="https://discord.gg/p6KqD2kjtB"><img src="https://img.shields.io/discord/1120774652915105934?style=social&logo=discord" alt="Discord"></a>
  <a href="https://github.com/SciPhi-AI"><img src="https://img.shields.io/github/stars/SciPhi-AI/R2R" alt="Github Stars"></a>
  <a href="https://github.com/SciPhi-AI/R2R/pulse"><img src="https://img.shields.io/github/commit-activity/w/SciPhi-AI/R2R" alt="Commits-per-week"></a>
  <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-purple.svg" alt="License: MIT"></a>
</p>

<img src="./assets/r2r.png" alt="R2R Answer Engine">
<h3 align="center">
The ultimate open source RAG answer engine
</h3>

# About
This is my configuration for [R2R](https://github.com/SciPhi-AI/R2R), which lets you use AI to retrieve information from documents. I create the necessary docker containers to run the application and set up local ollama LLM with tinyllama.

For a more complete view of R2R, check out the [full documentation](https://r2r-docs.sciphi.ai/).

# Run

I set up a docker container with postgres and neo4j already configured. You can run the container with
```bash
sudo docker compose up --build
```

To run the application, make sure you have all the python dependencies installed
You need poerty and python to run the application, on nixos `shell.nix` can be used to create your dev environment:
```bash
nix-shell
```
You can install the dependencies with
```bash
poetry install -E all
```

You then have to export all the variables in `.env`. Note that if you want to change a variable, you have to change also `docker-compose.yaml`.

To use a local model, you need [Ollama](https://github.com/ollama/ollama) and a model downloaded. You can start ollama with:
```bash
sudo ollama serve
```

You are now ready to go

# Usage

All the following command must be prepended with `porety run` or you can run `poerty shell` once and run the commands in the shell.

### !!!
If you are using ollama, you need to add `--config_name=local_ollama` after each command and `--rag_generation_config='{"model":"ollama/tinyllama"}'` after each `rag` command, with the model you want to use.

The configs are stored in `r2r/examples/configs/`. Some sample data is inside `r2r/examples/data/`.

<details open>
<summary><b>Document Ingestion and Management</b></summary>

1. **Ingest Files**:
   Here we are training the model on this files
   ```bash
   python -m r2r.examples.quickstart ingest_files
   ```

2. **View Document Info**:
   List the documents ingested
   ```bash
   python -m r2r.examples.quickstart documents_overview
   ```

3. **View User Overview**:
   ```bash
   python -m r2r.examples.quickstart users_overview
   ```
</details>

<details open>
<summary><b>Search and RAG Operations</b></summary>

1. **Search Documents**:
   Get the documents relevant to the query
   ```bash
   python -m r2r.examples.quickstart search --query="Who was Aristotle?"
   ```

2. **RAG Completion**:
   Get completition (an answer) to the query
   ```bash
   python -m r2r.examples.quickstart rag --query="What was Uber's profit in 2020?"
   ```

3. **Streaming RAG**:
   ```bash
   python -m r2r.examples.quickstart rag --query="What was Lyft's profit in 2020?" --stream=true
   ```

4. **Hybrid Search RAG**:
   ```bash
   python -m r2r.examples.quickstart rag --query="Who is John Snow?" --do_hybrid_search
   ```
</details>

For more detailed examples and advanced features, please refer to our [Quickstart Guide](https://r2r-docs.sciphi.ai/quickstart).

# R2R Dashboard

Interact with R2R using our [open-source React+Next.js dashboard](https://github.com/SciPhi-AI/R2R-Dashboard). Check out the [Dashboard Cookbook](https://r2r-docs.sciphi.ai/cookbooks/dashboard) to get started!

