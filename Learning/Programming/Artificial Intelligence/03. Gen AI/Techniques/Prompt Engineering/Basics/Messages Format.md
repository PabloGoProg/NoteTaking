Formats to write out prompts in code.

---
## Open-AI Messages Format (Most Common)
Open AI use a simple JSON structure with a list of messages, where each message has `content`, and `role` fields.

```JSON
{
	"messages": [
		{
			"role": "system",
			"content": "You are a helpful assistant..."
		},
		{
			"role": "user",
			"content": "What is the capital of france?"
		}
	]
}
```

- Role could be `user`, `assistant` or `system`.
	- `system`: High level instructions to influence LLM behavior.
	- `user`: Records prompts sent by users.
	- `assistant`: Records responses previously generated.

**When you develop a multi turn conversation**, you feed the LLM with the whole messages list in plain text formatted with special _text tags_.

![[Pasted image 20260608103145.png]]

### The System Prompt
The system prompt is commonly composed of two main sections:
1. _High Level Instructions_: Fundamental behavior and knowledge cutoff.
2. _Tone and Personality_: Define how LLM should communicate in terms of redaction style.
