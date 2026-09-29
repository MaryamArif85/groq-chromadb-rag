# RAG Chunking & Retrieval Guide

## Why Chunking is Critical
Too large = exceeds embedding limits, dilutes meaning
Too small = loses context, increases cost
Poor boundaries = splits related concepts, degrades retrieval

## Strategy Selection Decision Path
1. Start with recursive splitting at 256-512 tokens, ~15% overlap
2. Structured docs (PDFs, tables, code, HTML)? Add document-type aware parsing (Unstructured/Marker)
3. Heterogeneous density / mixed topics? Move to semantic chunking
4. Multi-hop or long-document QA? Add hierarchical small-to-big
5. Retrieval still weak? Try late chunking
6. Always measure with Ragas/DeepEval

## Tools
- chonkie: Token, sentence, recursive, semantic, late - fast batch indexing
- LangChain RecursiveCharacterTextSplitter: General-purpose default
- LlamaIndex SemanticSplitterNodeParser: Coherent chunks for narrative
- semchunk: Statistical semantic, low-cost

## Code Example
from langchain.text_splitter import RecursiveCharacterTextSplitter
splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=50,
    separators=["\n\n", "\n", ".", " "]
)
chunks = splitter.split_text(document)

## Future: Agentic RAG, Corrective RAG (CRAG), GraphRAG