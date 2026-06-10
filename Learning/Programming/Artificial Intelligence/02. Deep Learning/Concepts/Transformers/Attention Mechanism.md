Attention is a fancy way of saying "_which other tokens have the biggest impact on my meaning?_".

![[Pasted image 20260607170850.png]]

In this case, the `token` dog gives the most of its attention to the tokens `brown` and `sat` as those tokens are directly related to him in the context of the sentence.

---
## The Distribution of Attention

> An embedding model commonly returns two vectors for each token: `1. First Meaning Vector` that returns the first guess of the meaning of a token, and `2. The positional Vector`, that represents the position of the token in the prompt.

The mechanism used to distribute this attention is called an _Attention Head_. Most [[Transformer Architecture|Transformer Architectures]] use many attention heads, that specialize in different type of relationships between words. 

![[Pasted image 20260607171536.png]]

- Small models use 8 to 16 heads, while big models use more than a hundred.

Once all the attention values are set, the `First Meaning Vector`, the `Positional Vector` and the `Anttention Values` goes through the _Feed Forward Phase_: This phase take the inputs above and generate new meaning token embeddings for each token, that are **influenced by the context of the other tokens in the prompt**. -> The process of attention + feed forward phase occurs `N` time (Commonly 8 to 64) before generating.

![[Pasted image 20260607172748.png]]

Once all of this is done, the model ask itself "_Based on my training data, what is the token that is most likely to come next?_" -> To solve this answer, the transformer, as output, generated a probability distribution of all the vocabulary, where the most probable tokens are the most likely to be chosen, where the first token is the most commonly chosen (_Even if in theory all tokens has a small chance to appear_).

- Then, the selected token is added to the end of the input text.
- To select a new token, the whole process must be done again, using the input text with the generated tokens as input.
- This process is repeated until a generation limit is reached or the model selects a special token `EOS -> End of Sequence`.

![[Pasted image 20260607173631.png]]

