The retriever is the component that gets relevant information according to a user prompt and an specific knowledge base.

![[Pasted image 20260522070613.png]]

## Process of the Retriever

1. Process the prompt to understand its underlying meaning.
2. Use the understanded meaning to find the index of "relevant" documents.
3. (_Index Search Ends_) -> The retriever obtain the most relevant documents to the prompt.
4. The retriever ranks the relevance of each found document according to the prompt. (Some measure of the similarity between the texts of the prompt and the document).

---
## Search Techniques / Approaches

Search approaches look for documents using different strategies. _Metadata filtering_ excludes documents from the search based on _rigid criteria_.

![[Pasted image 20260522095841.png]]

- _Keyword search_ ensures sensitivity to exacto words included in the user prompt.
- _Semantic search_ looks for documents with similar meaning even without the same words.

**Hybrid Search**: Involves using both keyword and semantic search with a layer of metadata filtering.

![[Pasted image 20260522100938.png]]