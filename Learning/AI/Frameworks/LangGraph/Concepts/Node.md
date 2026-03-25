_Nodes_ are individual functions or operations that can perform specific tasks within the graph.

Each node _receives inputs_ (often the current state of the graph), process it and produces an output or and _updated [[State]].

```python
def greeting_node(state: AgentState) -> AgentState:
	state['user_message'] = "Hey " + state['user_message'] + ", how are you?"
	return state
```

## Types of Nodes

**Start Node**: Is the virtual entry point in LangGraph. marking where the flow begins. -> It _doesn't perform any operations itself_, but serves as the designated starting position for the graphs execution. 

**End Node**L Signifies the conclusion of the workflow in LangGraph. Upon reaching this node, the graph's execution stops, indicating that all the intended processes have been completed.

