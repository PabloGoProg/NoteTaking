This process involves data collection and preparation, using an appropriate algorithm, training the model and evaluate it.

![[Pasted image 20250212114956.png]]
### Training Data
The process begins collecting and preparing data. Bad data is often called _Garbage in, Garbage Out_, and therefore an ML model is only as good as the data used to train it. - Critical stage which determine if the model model works as intended or is ruining its performance.

* _Labeled data:_  label or target that represents the desire output or classification.
* _Unlabeled data:_ raw input features.
* _Structured data:_ organized and formatted in an predefined manner - suitable for traditional ML which needs well-defined features and labels.
	* Tabular data: databases or CSV files.
	* Time-Series data: values measured in successive points in time.
* _Unstructured data:_ lacks of predefined structure or format (text, images. audio, etc) - This type of data requires more advanced ML techniques to extract meaningful patterns and insights.
	* Text data: docs, articles, social media posts, etc.
	* Image data: digital images, photos or video frames.

### Machine Learning Process
Once we have the training data, this fed into a _machine learning algorithm_ - traditionally divided in three broad groups:

1. Supervised Learning: Trained with labeled data - learn a mapping function to predict outputs for new data.
	1. Classification
	2. Regression
2. Unsupervised Learning: Learns from unlabeled data - discover inherit patterns, structures o relationships within the input data.
	1. Clustering
	2. Dimensionality Reduction
3. Reinforcement Learning: Performance score as guidance, the agent feedback is provided in form of penalties or awards in order to improve the decision making over time - _semi-supervised learning_ uses just a fraction of labeled data.

### Inferencing
Once the model is trained, hes able to make predictions or decisions -- This is called _inferencing_.

* _Batch inferencing:_ Speed is not crucial - large amounts of data -> provide a set of results (batches).
* _Real time inferencing:_ Speed is crucial - complete response to new information as it comes.


## Deep Learning Fundamentals
In deep Learning we use Neural Networks that are computational models that mimic the human brain behavior - These contains layers of nodes (neurons) and each neuron of a layer are connected with one or more nodes of the next layer -- This model contains one _input layer_, one or more _hidden layers_ and an _output layer_. 

![[Pasted image 20250212145916.png]]

-- When a Neuronal Network recognize patterns, it can see to completely new samples and can still make predictions of how they might behave.

## Amazon AI Tools

![[Pasted image 20250213090411.png]]

### When are AI /ML solutions useful?
AI and ML solutions are commonly useful when the coding rules to be developed are more that challenging and the task can't be solved using rule-based-solutions. Also, AI is a good choice when the number of repetitions to make is much bigger than the approachable for humans.

_Sample:_ Detect Spam Mail Messages
4. Classify as email as spam is not a task that could be properly solved by rule-based solutions.
5. If classify 100 mails by a human could take much time, imagine millions.
