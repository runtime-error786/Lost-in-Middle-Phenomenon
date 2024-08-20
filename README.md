# Lost in the Middle Paper Solution

This repository contains the implementation of a solution to the "Lost in the Middle" problem using LangChain and other relevant tools. The solution focuses on efficiently retrieving relevant context from large documents and answering queries using an LLM (Large Language Model).

## Overview

The "Lost in the Middle" problem refers to the challenge of maintaining relevant context when dealing with large inputs that exceed the maximum context window size of language models. This implementation uses document splitting, embedding generation, and a retrieval system to address this issue.

## Solution Components

1. **Document Loading:**
   - The documents are loaded using the `PyMuPDFLoader` from LangChain, which allows for reading PDFs and extracting text content.
   - Two sets of documents are loaded from specified paths.

2. **Text Splitting:**
   - The documents are split into manageable chunks using `RecursiveCharacterTextSplitter` with a chunk size of 500 characters and an overlap of 100 characters. 
   - The text is converted to lowercase for uniformity.

3. **Embedding Generation:**
   - Embeddings are generated using the `HuggingFaceEmbeddings` model "sentence-transformers/all-MiniLM-L6-v2".

4. **Vector Stores:**
   - The document chunks are stored in Chroma vector stores for efficient retrieval.

5. **LLM Integration:**
   - The `Ollama` LLM is used for querying and answering based on retrieved contexts.

6. **Retrievers and Compressors:**
   - Multiple retrievers (`gen_retriever` and `rl_retriever`) are used and merged into a single retriever (`MergerRetriever`).
   - A document compression pipeline is applied using `EmbeddingsRedundantFilter` and `LongContextReorder` to remove redundant information and reorder content for long contexts.
   - The final retriever is created using `ContextualCompressionRetriever` for enhanced context retrieval.

7. **Question Answering Chain:**
   - A `RetrievalQA` chain is created using the compressed retriever and LLM to answer questions.
