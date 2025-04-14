TF-IDF (Term Frequency-Inverse Document Frequency) is a numerical statistic used in information retrieval to reflect how important a word is to a document in a collection. It's a fundamental concept in sparse retrieval methods and consists of two components that work together:

### Term Frequency (TF)

- Measures how frequently a term appears in a document
- The idea: Words that appear often in a document are likely important to that document
- Formula: `TF(term, document) = (Number of times term appears in document) / (Total number of terms in document)`
- Example: If "AI" appears 5 times in a 100-word document, TF = 5/100 = 0.05

### Inverse Document Frequency (IDF)

- Measures how rare or common a term is across all documents
- The idea: Rare terms across all documents are more discriminative and informative
- Formula: `IDF(term) = log(Total number of documents / Number of documents containing the term)`
- Example: If "AI" appears in 10 out of 1,000 documents, IDF = log(1000/10) = log(100) ≈ 2

### How They Work Together

- TF-IDF is the product of these two metrics: `TF-IDF = TF × IDF`
- This gives higher weight to terms that:
  1. Appear frequently in a specific document (high TF)
  2. But are rare across the entire collection (high IDF)
- For example, common words like "the" or "and" will have very low IDF scores, while specialized terms like "transformer architecture" will have high IDF scores

### Why It's Powerful

1. **Penalizes Common Words**: Words like "the," "is," "of" have high TF but very low IDF, so their TF-IDF score is low
2. **Rewards Distinctive Words**: Terms that characterize a document uniquely get higher scores
3. **Document Length Normalization**: TF normalizes by document length, so longer documents don't automatically get higher scores

### How It's Used in Retrieval

1. **Indexing**: Calculate TF-IDF scores for every term in every document
2. **Query Processing**: Represent user queries as TF-IDF vectors
3. **Matching**: Calculate similarity (often cosine similarity) between query vector and document vectors
4. **Ranking**: Return documents with highest similarity scores

Despite being decades old, TF-IDF remains remarkably effective for many retrieval tasks, especially when exact term matching is important. Modern systems often use it alongside newer embedding-based approaches or as part of more sophisticated algorithms like BM25 (which is an enhanced version of TF-IDF that handles term saturation and document length normalization better).
