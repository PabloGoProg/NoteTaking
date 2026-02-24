The _State_ is a shared data structure that _holds_ the current information or context of the entire application. -> Is like application memory, keeping track of variables and data that nodes can access and modify as they execute.

### How to Create an Agent State

```Python
from typing import Dict, TypedDIct

# `total=False` allows the idct values to be optional (default behavior)
class AgentState(TypedDict, total=False):
	user_message: 
```

