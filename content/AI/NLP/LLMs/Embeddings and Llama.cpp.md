# Embeddings and Llama.cpp

### SQLite VSS - Lightweight Vector DB

[SQLite VSS](https://github.com/asg017/sqlite-vss) is a SQLite extension that adds vector search on top of SQLite. It's based on FAISS[<sup>1</sup>](https://observablehq.com/@asg017/introducing-sqlite-vss)

There are some examples of how to use Pure SQLite VSS on the blog post [here](https://observablehq.com/@asg017/introducing-sqlite-vss)

### LangChain

You can use SQLite VSS with Langchain which makes it easier to use. The documentation is [here](https://python.langchain.com/docs/integrations/vectorstores/sqlitevss) for sqlite-vss and [here](https://python.langchain.com/docs/integrations/text_embedding/llamacpp) for using llama for embedding.

You need to install `sqlite-vss` python package to use it via `pip install sqlite-vss`

#### Zephyr embeddings

Load the zephyr model with long contet and set gpu layers up.

```python
llama = LlamaCppEmbeddings(model_path="/path/to/models/zephyr-7b-alpha.Q5_K_M.gguf", 
            n_batch=512,
            verbose=True, # Verbose is required to pass to the callback manager
            n_ctx=16000,
            n_gpu_layers=32)
```

NB: I found that Zephyr isn't actually very good for generating embeddings - I suppose this is likely because it is fine-tuned for chatting rather than for embedding.

It actually turns out that the default [MiniLM](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) that comes with sentence-transformers does a pretty reasonable job:

```python
embedding_function = SentenceTransformerEmbeddings(model_name="all-MiniLM-L6-v2")
```