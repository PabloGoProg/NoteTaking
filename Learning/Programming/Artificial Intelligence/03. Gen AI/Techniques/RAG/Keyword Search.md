KW Search is an approach that look for documents that _contains shared words with the user prompt_. -> Documents that contains more words from the user prompt are _more likely_ to be relevant for the answer.

- The order of words doesn't matter at all, only word presence and frequency does.
- Each prompt and document are converted to a _Sparse Vector_ -> This vector contains one spot for each word in the system vocab, and store how often the word appears in the piece of text.
- We can arrange all documents _Sparse Vectors_ is a single matrix **Term Document Matrix (TDM)**, with a size of `n by m`, where `n` are the words in the vocab and `m` are number of documents.

![[Pasted image 20260522103325.png]]

## Process and Techniques for Ranking Documents

