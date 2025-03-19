## Agent Execution Chain
Is know as the process that happens between we give the input to the agent and it return the answer.

`Propmt input -> [ Agent Execution Change ] -> Final Answer`

This process consists of 4 steps
1. **Thought** -> _Which sub-tasks can be derived from the input task?_ -> Order them by priority of execution. 
2. **Action** -> Which action needs to be execute to complete each sub-task?
3. **Pause** -> Perform the chosen actions and then pause.
4. **Observation** -> When the agent pauses, then he starts "reasoning" with itself

_This process is repeated over a number of iterations before to return the final answer_

## Tools and Memory
AI Agents have access to what we call _Tools and Memory_ to:
* Tools -> Interface with external world systems as databases or API's.
* Memory -> Remember all preferences or previous interactions.