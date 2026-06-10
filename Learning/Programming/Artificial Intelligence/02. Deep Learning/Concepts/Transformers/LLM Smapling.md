Different parameters of a language model (LLM) impact its output. Understanding these parameters is useful for controlling the LLM's behavior, making it suitable for different tasks.

See [[Attention Mechanism]] to understand how LLMs generate new text.

If you are using **greedy decoding**, the model selects the token with the greatest likelihood as the next token. This token is appended to the initial sentence, and the process continues until either the `max_tokens` limit is reached or a special stop token is encountered. -> It's important to note that greedy decoding is **deterministic**.

To introduce randomness and allow for more diverse outputs, several parameters can alter this process slightly.

---
## Nucleus Sampling - `top_p`

The LLM randomly choose one among the **p** most likely tokens—based on their probability distribution. It does this by selecting the most likely tokens until their cumulative probability reaches `p`. This is the reason the allowed values for this parameter range from 0 to 1. Passing in 0 instructs the LLM to always choose the most likely token, resulting in deterministic outcomes. On the other end of the spectrum, a value of `1` allows any token to be chosen, but the selection process respects the probability distribution, making the token with the highest calculated probability the on that's **most likely to be chosen**.

### Examples

**Top-p of 0**:

```
Call number 1:
Response: RAG (Retrieval Augmented Generation) is a technique that enhances the accuracy and relevance of an AI's responses by first fetching external information from a knowledge base and then using that retrieved data to inform its generated output.

Call number 2:
Response: RAG (Retrieval Augmented Generation) is a technique that enhances large language models by dynamically retrieving relevant external information from a knowledge source and using it to inform the model's response, thereby improving accuracy and reducing hallucinations.

Call number 3:
Response: RAG (Retrieval Augmented Generation) is an AI technique that enhances the accuracy and relevance of generated responses by dynamically fetching and integrating external, up-to-date information from a knowledge base before synthesizing an answer.
```

**Top-p of 0.8**:

```
Call number 1:
Response: RAG (Retrieval Augmented Generation) is a technique that enhances the accuracy and relevance of an AI's responses by first fetching external information from a knowledge base and then using that retrieved data to inform its generated output.

Call number 2:
Response: RAG (Retrieval Augmented Generation) is a technique that enhances large language models by dynamically retrieving relevant external information from a knowledge source and using it to inform the model's response, thereby improving accuracy and reducing hallucinations.
Call number 3:

Response: RAG (Retrieval Augmented Generation) is an AI technique that enhances the accuracy and relevance of generated responses by dynamically fetching and integrating external, up-to-date information from a knowledge base before synthesizing an answer.
```

## Top-k sampling

**top-k** sampling focuses on the number of candidates. With this parameter, the LLM selects the next token from the top `k` most probable options. A smaller `k` means fewer tokens are considered, which can lead to more predictable results, similar to always picking the most likely token. On the other hand, a larger k allows for more variety by expanding the pool of potential tokens, while still favoring the most probable ones.

## Temperature

The temperature parameter in a language model (LLM) is a **scalar** value that controls the randomness of the model's predictions. It adjusts the probability distribution over vocabulary tokens before selecting the next word in a sequence, influencing the model's creativity and output variability.

Let's consider a probability vector $[0.3, 0.6, 0.1]$. The temperature modifies these probabilities by applying the following formula to each element in the vector:

$$\mathrm{adjusted\_probability}(p_i) = \frac{\exp(\log(p_i) / \mathrm{temperature})}{\sum \exp(\log(p_i) / \mathrm{temperature})}$$

- This involves:
  - Scaling the logarithm of each probability by dividing it by the temperature.
  - Exponentiating the result to obtain a new probability.
  - Normalizing the probabilities so they sum to 1 again.

### Effects of Different Temperature Values:

- **Low Temperature (<1):**
  - Sharpens the probability distribution.
  - Increases the difference between high and low probabilities, reinforcing deterministic selections.

- **High Temperature (>1):**
  - Flattens the distribution.
  - Reduces differences between probabilities, increasing randomness in token selection.

- **Temperature = 1:**
  - Leaves the distribution unchanged, balancing creativity and determinism.

**Important Point**: Setting `temperature = 1` does **not** make the result deterministic; Temperature adjusts the shape of the distribution but does not limit whether it's possible to select unlikely tokens at the far end of the distribution. Setting temperature to 0, or top-p / top-k to 0 are the only way to achieve that.

### Example:

Consider the original token probability vector $[0.6, 0.3, 0.1]$:

- **Temperature = 0.5 (Low):**
  - Result vector: $[0.77, 0.18, 0.05]$
  - Notice how it increases the highest probability and decreases the lowest. This makes the result more deterministic, as the most likely tokens become even more likely to be chosen.

- **Temperature = 1 (Neutral):**
  - Result vector: $[0.6, 0.3, 0.1]$
  - The probability distribution remains unchanged.

- **Temperature = 2 (High):**
  - Result vector: $[0.49, 0.27, 0.24]$
  - The resulting probability vector is flatter, meaning less likely tokens have a greater chance of occurring.

Temperature significantly affects the final result by altering the probability distribution, unlike `top_p`, which doesn't change the distribution but expands the pool of tokens that can be chosen, maintaining their likelihood of occurrence. High temperature values may lead to nonsensical text.

## Repetition penalty

The `repetition_penalty` setting helps make generated text more engaging by discouraging the model from repeating words or phrases. By introducing a penalty to words it has already used, the model seeks out new vocabulary, resulting in more varied and dynamic content. -> high repetition penalty can make the text sound nonsensical because it makes the model avoid using the same words too often.