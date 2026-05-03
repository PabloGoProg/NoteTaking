Large Language Models are [[Foundational Models]] can be based on a variety of architectures -- The most common nowadays is the [[Transformers]] architecture, giving models capable of understand and generate human-like text.

__Tokens__: are the basic unit of the text processed. -- can be words phrases or individual chars.

![[Pasted image 20250212161800.png]]

**Embeddings:** Theses are numerical representations of tokens, where each token are assigned with a vector -- Vectors are learned during the training process and are the ones that allow model to understand context and relationships between tokens.

![[Pasted image 20250212162303.png]]

### Diffusion Models
Deep Learning Arch System that starts with pure noise or random data -> models _gradually_ adds more and more meaningful info to this noise until ends with a coherent output. -- This models learns with a two-step process:

1. _Forward Diffusion:_ introduces _noise_ until noise is left over.
2. _Reverse Diffusion:_ gradually _denoise_ until a new image is generated.

### Multimodal Models
This models are prepared to process and generate multiple types of data.

`input (image + text) -> process -> output (image + text caption)`

This models learn from how the different kind of data are connected and how them can influence each other. 

## Amazon Gen AI Tools

![[Pasted image 20250213090440.png]]

### Considerations for implementing AI on a project
1. Model Type -> Type of LLM.
2. Performance -> Accuracy, reliability, etc.
3. Constraints -> Hardware, data, deployment requirements.
4. Capabilities -> Actions that can perform.
5. Compliance -> Follows Moral Concerns.
6. Cost -> Size & Speed trade off.

### Business Metrics for Gen AI Applications
1. User satisfaction
2. Average Revenue per User
3. Cross-domain performance -> ability to perform properly on different industries.
4. Conversion rate -> Transform application into desire outcomes.
5. Efficiency -> resource utilization, computation time and scalability.