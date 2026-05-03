General purpose models that are pretrained with internet scale data (_foundation model_). Preparing models to perform multiple tasks between text generation, text summarization, information, extraction, etc. -> We say FMs are pretrained, cuz the can be fined tuned for specific actions.
#### Foundational Models - Life Cycle
1. _Data Selection:_ Unlabeled data is easier to find that labeled - can be used at scale - needs diverse sources of data.
2. _Pre-training:_ In classic ML, models are trained to match information to a label -- When we use unlabeled data we can make self-supervised learning, which means "Getting labeled data from unlabeled data". Here the model can understand the context, meaning, and relationships between the words -- once finished, the model can be involved in _continuous pre-training_ with the goal of expand base knowledge and generalize across different domain of tasks.
3. _Optimization:_ FMs can be optimized in different techniques as prompt engineering, retrieval-augmented-generation (RAG) and Fine-Tuned on specific tasks.
4. _Evaluation:_ An FMs performance can be measured using appropriate metrics and benchmarks.
5. _Deployment and further improvement._