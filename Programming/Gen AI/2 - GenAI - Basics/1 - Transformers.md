Initially developed in 2017 by Google with the focus of translating a peace of text from one language to another.

`Hola Mundo -> [ Google Transformer ] -> Hello World`

Nowadays - and more specifically - the ==transformers== used for LLMs like ChatGPT are designed to receive a piece a text (maybe with other kind of data accompanying it) and try to produce a prediction of whats next. ==This prediction takes form of a probability distribution== over a set of text chunks that may follow.

Transformers are computational neural networks that contains the next layers:

**IMPORTANT:** All this explanation in based on GPT-3 Model.
## 1. Embedding Matrix
First we need to know that GPT's model has a base vocab, including more than 50k words, here, the first matrix we'll find in the model is the embedding matrix [[3- LLMs]], which contains a column for each token on the vocab. Each value of this matrix is know as `weight`, which are the final values learned from the training process.

```
[
  w1 | wn + 1 | . . . | wn(m - 1) + 1
  w2 | wn + 2 | . . . | wn(m - 1) + 2
  w3 | wn + 3 | . . . | wn(m - 1) + 3
  w4 | wn + 4 | . . . | wn(m - 1) + 4
  .  | .      | . . . | .
  .  | .      | . . . | .
  .  | .      | . . . | .
  wn | w2n    | win   | wnm
]
```

Its crucial to know that the _dot product_ between two embeddings represents the semantic connection between those two.
- if the result is positive, the the vectors points similar directions.
- if the result is 0, the vectors are perpendicular one to each other.
- if the result is negative, the vectors points opposite directions.

At the beginning, when we create the array of vectors based on the input, ==each one of those is only able to encode the meaning of the single word==  without any input from the surroundings (context).



