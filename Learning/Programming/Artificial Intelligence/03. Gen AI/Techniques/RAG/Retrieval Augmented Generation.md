Retrieval Augmented Generation (RAG) is an approach that further improves the performance of large language models by giving the access to information that don't know from the training.

---
## Why RAG are Important for LLM Based Applications

_The response of an LLM is as good as the information they have_. -> When we prompt an LLM, we prompt a mathematical model that answers based of the training information:

The issue?

1. The model could have been not trained for the task the user is requesting.
2. The request could need newer information that the training process used.
3. The request could require expert level on certain topic, domain specific information or enterprise private information to answer properly.

RAG systems propose to _collect information_ and _reason and respond_ using the collected info before generating the answer.

`[1. User Prompt] -> [2. RAG System] -> [3. Augmented Prompt] -> [4. LLM]`

**Note**: An _augmented prompt_ is the combination of the user prompt and the retrieved information.

---
## RAG Components

![[Pasted image 20260510203021.png]]

