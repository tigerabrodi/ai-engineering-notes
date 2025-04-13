# Chapter 6: RAG (Retrieval-Augmented Generation)

## Core Concepts of RAG

**Why RAG Remains Important**:

- Even with expanding context windows, RAG provides crucial benefits:
  - Focuses model attention on relevant information
  - Provides access to information beyond model training data
  - Enables real-time knowledge updates without retraining

**RAG Architecture Components**:

1. **Retriever**: Finds and retrieves relevant information
2. **Generator**: Creates responses using the retrieved information

## Document Processing for RAG

**Chunking Strategy**:

- Breaking large documents into manageable pieces
- Critical when documents exceed context limits
- Balance between chunk size and semantic coherence

## Retrieval Mechanisms

### Term-Based Retrieval (Sparse Retrieval)

- **How it works**: Uses frequency of terms/keywords for matching
- **Common algorithms**: TF-IDF, BM25
- **Vector representation**: Sparse vectors (mostly zeros)
  - Each dimension represents a specific word in vocabulary
  - Only terms in the document have non-zero values
- **Strengths**:
  - Highly interpretable (clear which terms matched)
  - Computationally efficient
  - Excellent for exact keyword matching
  - Works well with specialized terminology
- **Limitations**:
  - Misses semantic relationships
  - Poor with synonyms or conceptually related terms
  - Vulnerable to vocabulary mismatch problems

### Embedding-Based Retrieval (Dense Retrieval)

- **How it works**: Uses neural networks to map text to semantic space
- **Common approaches**: Sentence transformers, embedding models
- **Vector representation**: Dense vectors (most dimensions have values)
  - Each dimension represents learned semantic features
  - Similar meanings have similar vectors regardless of specific words
- **Strengths**:
  - Captures semantic relationships between concepts
  - Handles synonyms and paraphrasing effectively
  - Better for conceptual understanding of queries
  - Can find relevant matches even with different terminology
- **Limitations**:
  - Less interpretable than sparse vectors
  - Requires more computational resources
  - More complex to implement and fine-tune

### Hybrid Approaches

- Combining sparse and dense retrieval for better results:
  - Initial filtering with fast sparse retrieval
  - Re-ranking with more powerful dense retrieval
  - Weighted combinations of both scoring methods

## Retrieval Optimization Techniques

- Query reformulation to improve search effectiveness
- Re-ranking retrieved results based on relevance
- Metadata filtering to narrow search space
- Adaptive retrieval based on query characteristics
