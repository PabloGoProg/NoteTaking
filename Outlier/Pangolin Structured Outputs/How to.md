# Steps to Make a Task

1. Read the full user message carefully. Understand what the user wants and how to make it.
	1. Write the _System Prompt_ for the model. 
		1. Give him a role.
		2. State the wanted action (generate, extract, transform).
		3. Includes background or rules if needed.
		4. **AVOID HARM PROMPTS**
2. Define the JSON Schema of the Output
	1. Select the correct Schema Type:
		1. Non-recursive Object -> Structures that do not repeat elements.
		2. Recursive Object -> Structures that may need the repetition of elements.
		3. Array of Objects -> List of something (Object: ej. Employee).
		4. Array of Strings -> List of names or things that are not needed to be compound objects.
3. Prepare User Prompt
	1. Localized in USA
	2. Don't mention LLM comercial names, instead just named them as LLMs.
	3. Include JSON Schema after prompt.
	4. State the wanted action (generate, extract, transform).
	5. Qualify the toxicity of the text:
		1. _Benign_ -> Could produce harmful content but do not seek it.
		2. _Harmful_ -> Contains harmful content or aims to assist or enable harmful actions. 
		3. _Critical_ -> Harmful texts that aims to bypass the safety protections.
	6. Prompt Risk Level
		1. High -> Prompts that mainly leads to harmful actions.
		2. Low -> Can lead to harmful responses but exists ways to avoid them.
4. Rewrite the prompt:
	1. Reroll the response if the response is off-topic and the tasks allow it.
	2. If the response is usable, denote errors in the next step.
	3. Ensure the response matches the JSON Schema -> Fix it if not.
	4. Select Rewrite Strategy
		1. Full engagement -> Respond to the full prompt.
		2. Deflection -> Be helpful, but redirect the user out from harmful or restricted actions.
		3. Partial -> Respond cautiously, with limited scope.
		4. Decline -> Refuse to answer -> “Unable to work with that request.ˮ
