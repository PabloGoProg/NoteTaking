A _Graph_ in LangGraph is the overarching structure that maps out how different tasks ([[Node]])s are connected and executed. -> A graph can visually represents the workflow, showing the sequence and conditional pats between operations.

**Edges**: The edges are the connections between nodes that determine the flow of execution. They tell us which node should be _executed next_ after one completes its task.

**Conditional Edges**: Specialized connections that decide next node to execute based on specific conditions or logic applied to the current state.

## State Graph

A _State Graph_ is a class in LangGraph used to _build and compile_ the graph structure. -> It manages the nodes, edges and the overall state of the graph, ensuring that the workflow operates in a unified way and the data flows correctly between components.

```Python
def build_graph() -> StateGraph:
	graph = StateGraph(AgentState)
	graph/add_node('greeter', greeting_node)
	
	graph.set_entry_point(greeting_node)
	graph.set_finish_point(greeting_node)
	
	app = graph.compil
	
```