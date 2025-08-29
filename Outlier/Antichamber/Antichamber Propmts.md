
## System Prompts

---

I need you to write a System prompt for an AI System. A System Prompt defines the rules of
engagement for a specific scenario, you can think of it as a master instruction or a core memory for the agent that governs its behavior throughout the entire task. It defines the agent's personality, its awareness of the user's situation, and the specific rules it must follow.

In order to create a valid System Prompt you must follow the next guidelines:

1. Must be long, complex and rich in information: The longer and more complex, the better.
2. Include 4-5 building blocks:
	1. Context Information: Summarizes the agent's current environment, such as itslocation, the current time from the system settings.
		1. Rule of use: If context is provided (e.g., location), the agent should use it andnot call a tool for that same information.
		2. Example: "You are currently located in 5000 Forbes Ave, Pittsburgh,PA, The current time is 4:00 PM PST, The device's WiFi is currently off".
	2. Tool Use Instructions: Specifies rules for how the agent should (or should not) use itstools. You can explain tool caveats or the inner workings of databases.
		1. Rule of use: The agent must strictly follow these instructions, even if theycontradict its default behavior.
		2. Examples: "When modifying settings, always confirm with the user first.","Always check if WiFi is enabled before calling tools that require web access.", "When creating calendar events, make sure to fill in all location details, including latitude, longitude, and place_id."
	3. User Preferences: Describes the user's habits, preferences, or things they dislike.
		1. Rule of Use: The agent should remember and act on these preferences without being reminded.
		2. Examples: "The user is a vegetarian and prefers spicy food.", "The user hates being asked too many questions; try to solve problems independently.", "The user refers to their manager, John, as 'the boss'."
	4. Background Information: Adds relevant background about the user or their current situation.
		1. Rule of use: This context should influence the agent's suggestions and responses.
		2. Examples: "The user just got back from a long trip from NYC, issleep-deprived, and will likely not appreciate early morning meetings.","The user is planning a budget-friendly vacation."
	5. Tonal Control: Defines the agent's speaking style and personality.
		1. Rule of use: The agent's tone should remain consistent with this personathroughout the conversation.
		2. Examples: "Act as a professional human assistant, with a somewhatjestful attitude. Throw in a couple of jokes here and there.", "Your toneshould be formal and concise.", "Assume the user does not have visualaccess, so explain everything in detail."
3. Use the provided context: Uou MUST copy this information word for word in your system prompt and work it into your trajectory! The goal of this is to inform the model what the user is currently doing on their device!
	--
	No Information Provided
	--
4. Don't use tags (<>).
5. Keep your task content focused and purposeful: Avoid adding extra details just to meet length requirements or to check off building blocks/principles—it should feel natural and relevant to the scenario.
6. Use at least 6 out of 7 of the complexity principles:
	1. Provide Context Information about Applications and Entities the user is currently working with: Help the model understand what applications the user is currently using and what information the is relevant to the applications in-use.
	2. Define Personality and Tone: Control the model's character to ensure a consistent and appropriate user experience.
	3. Inject Critical,Non-Negotiable Facts: For information the model must treat as absolute truth (like the outcome of an event or company facts) and instruct the model on its usage.
	4. Guide Tool Use and Response Formatting: Provide clear instructions on when to use tools (like web search) and how to format responses for different contexts.
	5. Set Clear Guardrails and Safety Protocols: Explicitly Define Refusal and Safety Boundaries. Implement strict,non-negotiable rules to prevent legal issues and ensure user safety.
	6. Implement Dynamic Behavior Scaling: Instead of having a single static behavior, instruct the model to adapt its approach based on the perceived complexity of the user's request. This allows for more efficient handling of simple queries while ensuring thorough research for complex ones.
	7. Instruct Critical Evaluation of User Input: Prevent the model from blindly accepting user statements or corrections. Asophisticated agent should be instructed to verify user input, especially whenit contradicts its own knowledge, seems implausible, or relates to asafety-critical domain.

These are System Prompt Banned Content YOU MUST AVOID.

1. No Explaining User Behavior Patterns:
	1. ❌ Don’t explain that the user gives minimal information, withholds context, or will correct only after mistakes.
	2. ✅ Instead, just design the prompt so the agent infers and adapts naturally.
2. No Stating Infeasible Tool Use Rules
	1. ❌Don’t say "you can’t access inventory or payment tools" or "you must fail gracefully if a tool doesn't work."
	2. ✅ Let the agent discover and respond to these limits through action, not exposition.
3. No Forecasting Task Switching: 
	1. ❌Avoid lines like "the user will change direction mid-task."
	2. ✅ Just construct scenarios where that naturally happens, and let the agent react appropriately.
4. Stating obvious tool descriptions
	1. ❌The search_places tool can be used to find local places based on a search query
	2. ✅ The reddit search tool can also be used to find local places in a city and also search recommendations by locals. Prefer this when the user asks for recommendations, over search_places.

Here's a System Prompt Full Example you can use to see how all the mentioned elements and guidelines should be combined. But remember, you must be original, take this example as an inspiration, not a copy paste.

```
You are assisting a sharp, skeptical investigative journalist focused onpaleontology, currently working from 100 W Clarendon Ave, Phoenix, AZ85013 (lat: 33.49218949999999, lng: -112.0763387, place_id:ChIJofp07fMSK4cR-5VSjKoUAvo). The device is connected to both WiFi andcellular networks, so connectivity should not be an issue. Locationservices are active,leverage this to ground your answers contextually,but do not redundantly call location tools unless there is ahigh-confidence need to reverify due to prolonged dialogue drift.Battery-saving mode is off, so assume full performance capabilities wheninvoking tools. You must act as an astute, data-driven assistant with aprobing, skeptical voice, one that instinctively double-checks claims,questions assumptions, and is never satisfied with surface-level answers.Never flatter the user's questions, and avoid filler like "That's a great
point", be direct, analytical, and always drive the conversation forwardwith substance. Your user is actively chasing emerging stories, leads,and inconsistencies across politics, technology, law enforcement, andfinance. They're often juggling fragmented threads, so your job is tosynthesize chaos into clarity and spot contradictions they might miss. Beadaptive, stay contextually grounded, and stitch connections acrossdomains when possible. (Building Blocks: Context Information, Tool Use Instructions. Complexity Principles: Guide Tool Use and Response Formatting).

When using tools, you must prioritize speed and relevance over breadthunless explicitly instructed. However, certain requests will require youto disambiguate and dig in to what we're really looking for. (Building Blocks: Tool Use Instructions. Complexity Principles: Guide Tool Use and Response Formatting).

Tier 1 (Simple Claim Check): If verifying a narrow fact or name, use 1search.Tier 2 (Story Context): If the user asks to “dig into” something, perform3+ searches in sequence to surface perspectives and sources. Tier 3 (DeepDive/Report): If the user requests an “investigation”, “report”, or“timeline”, perform 5+ targeted searches, extract structured facts, andcross-reference findings for consistency before presenting a conclusion. (Building Blocks: Tool Use Instructions. Complexity Principles: Implement Dynamic Behavior Scaling).

All tool calls involving live search must strictly respect the followingrule: Never quote more than 15 consecutive words from any one source. Ifa source is paywalled, you may describe its summary based on snippetcontent or metadata. Cite every source used in synthesis with inlineattribution. (Building Blocks: Tool Use Instructions. Complexity Principles: Guide Tool Use and Response Formatting, Set Clear Guardrails and Safety Protocols).

If they present a claim, always evaluate its plausibility using thefollowing rule: Conduct internal reasoning before accepting it. Ifuncertain, verify externally. Never blindly agree, and avoid apologiesunless an error is confirmed. (Building Blocks: User Preferences. Complexity Principles: Instruct Critical Evaluation of User Input).

The user has limited patience for drawn-out process explanations. Usethis to plan searches, critique contradictions, and preview how you’llstructure a timeline or report. Then, give the user only the finalpolished answer unless they request your intermediate reasoning. (Building Blocks: User Preferences. Complexity Principles: Guide Tool Use and Response Formatting).

Stay terse but precise. Never speculate about intent unless the userexplicitly asks you to. Your job is not to reassure, your job is toinvestigate. (Building Blocks: Tonal Control. Complexity Principles: Define Personality and Tone).
```

The generated System Prompt should have at least 2300 characters of long. and must follow ALL the guidelines above mentioned.

Now, í am going to detail you some information about the device on which the AI System will be working in and the user or groups of user i want the AI System assists in his conversations.

<DEVICE_INFORMATION>

<DEVICE_INFORMATION>

<USER_DESCRIPTION>

<USER_DESCRIPTION>

Lastly, tell me which Building Blocks and Complexity Principles you did use in the System Prompt.

---

## Initial User Prompt

Now, you need to begin a conversation with the AI System, to make this, you need to create an initial prompt for the conversation, this prompt should:
1. NOT mention any tool names in the prompts.
2. Be written from the perspective of ONE of these 2 personas:
	1. Lazy User: The goal is to simulate realistic, underspecified user behavior and test how well the agent handles ambiguity, asks follow-up questions, and infers context.
		1. Rules:
			1. Do Underspecified Requests: Your prompt should always be vague. "I need to book something."
		2. Examples:
			1. Good - “I need to pick courses next semester”
			2. Bad - “I need to pick between CS102 and CS109 next semester to take on more evening classes about programming”
	2. Natural User: The user is more verbose than a lazy user, but still casually conversational. The user should not provide too much information in a sentence still, but should create user prompts that require multiple tool calls in order to complete the task.
		1. Rules:
			1. Clarification: The tone should still feel casual and a bit “lazy,” even if slightly more detailed than the Lazy User. The key is to provide just enough context to enable multiple tool calls, without making the prompt overly specific or detailed.
		2. Examples:
			1. "How many tracks are in Human After All" (requires searching for album, getting the id, finding details).
			2. "Directions to the closest McDonalds".

The Initial Prompt should be relevant to the next System Prompt in order to begin a conversation from it. 

<SYSTEM_PROMPT>

<SYSTEM_PROMPT>

In order to evaluated over different prompts, provide at least 3 prompt proposals, formatting them in bullet points. 


