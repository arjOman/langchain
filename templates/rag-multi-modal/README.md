# rag-multi-modal

This template performs RAG on documents with images.

It is confiured to ingest a pdf file that contains images:

* It uses uses [Unstructured](https://unstructured-io.github.io/unstructured/) for pdf parsing.
* It uses [Chroma](https://www.trychroma.com/) for stroage.

## Environment Setup

Set the `OPENAI_API_KEY` environment variable to access the OpenAI models.

[Unstructured](https://unstructured-io.github.io/unstructured/) requires some system-level package installations:

On Mac, you can install the necessary packages with the following:

```shell
brew install tesseract poppler
```

## Usage

To use this package, you should first have the LangChain CLI installed:

```shell
pip install -U langchain-cli
```

To create a new LangChain project and install this as the only package, you can do:

```shell
langchain app new my-app --package rag-multi-modal
```

If you want to add this to an existing project, you can just run:

```shell
langchain app add rag-multi-modal
```

And add the following code to your `server.py` file:
```python
from rag_semi_structured import chain as rag_semi_structured_chain

add_routes(app, rag_semi_structured_chain, path="/rag-multi-modal")
```

(Optional) Let's now configure LangSmith. 
LangSmith will help us trace, monitor and debug LangChain applications. 
LangSmith is currently in private beta, you can sign up [here](https://smith.langchain.com/). 
If you don't have access, you can skip this section

```shell
export LANGCHAIN_TRACING_V2=true
export LANGCHAIN_API_KEY=<your-api-key>
export LANGCHAIN_PROJECT=<your-project>  # if not specified, defaults to "default"
```

If you are inside this directory, then you can spin up a LangServe instance directly by:

```shell
langchain serve
```

This will start the FastAPI app with a server is running locally at 
[http://localhost:8000](http://localhost:8000)

We can see all templates at [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
We can access the playground at [http://127.0.0.1:8000/rag-multi-modal/playground](http://127.0.0.1:8000/rag-multi-modal/playground)  

We can access the template from code with:

```python
from langserve.client import RemoteRunnable

runnable = RemoteRunnable("http://localhost:8000/rag-multi-modal")
```

For more details on how to connect to the template, refer to the Jupyter notebook `rag-multi-modal`.