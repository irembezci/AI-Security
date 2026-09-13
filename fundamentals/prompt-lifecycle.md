# Prompt Structure and the Prompt Lifecycle

Understanding what a prompt is and how it becomes part of an LLM's context is important, but we can go one step further and examine how a prompt is structured and what happens to it before the model generates a response. A well-structured prompt can contain several different components. These components provide the model with information about what it should do, how it should behave and how the final response should be structured.

## Components of a Prompt

A prompt can contain different elements depending on the task. Some prompts may be very simple, while others can contain multiple instructions and constraints.

One common component is the **role**. The role defines who the AI should act as or what perspective it should use.

For example:

```text
You are a cybersecurity expert.
````

This instruction establishes a particular role for the model and can influence how it approaches the task and formulates its response.

Another component is the **task**. The task describes what the AI should actually do.

For example:

```text
Explain SQL injection.
```

The task gives the model a specific objective to perform.

A prompt can also contain **context**. Context provides relevant background information that helps the model understand the task.

For example:

```text
The application uses a PostgreSQL database and receives user input through a login form.
```

This additional information gives the model more information about the environment in which the task should be considered.

Another important component is **constraints**. Constraints define rules or limitations that the model should follow when generating its response.

For example:

```text
Keep the explanation under 100 words.
```

This tells the model how much information it should provide. 

Finally, a prompt can specify an **output format**. The output format defines how the response should be structured.

For example:

```text
Return the answer as a table.
```

The model can then organize its response according to the requested format.

These components can be combined into a single prompt:

```text
Role:
You are a cybersecurity expert.

Context:
The application uses a PostgreSQL database.

Task:
Explain how SQL injection can occur in this application.

Constraints:
Keep the explanation under 100 words.

Output Format:
Return the answer as a table.
```

The important idea is that these components work together to provide the model with a clearer description of the desired behavior. A well-structured prompt does not necessarily need to contain every component. The required components depend on the task.


## Prompt Lifecycle

After a user provides a prompt, the system does not simply pass the raw text directly to the LLM and immediately receive a response. The prompt goes through several stages before the final response is generated. The process begins with **user input**. The user provides a prompt containing a question, instruction or task.

```text
User Input
      ↓
"How do I reset my VPN password?"
```

The system then receives the prompt during **prompt reception**. At this point, the application can process the input and determine what additional information may be required to answer the request. The next stage is **context assembly**. The system gathers the information that is relevant to the current request.

This can include:

```text
System Instructions
+
User Prompt
+
Conversation History
+
Retrieved Information
+
Tool Results
```

These pieces of information are combined into the context that will be provided to the model. The next stage is **tokenization**. LLMs do not process text exactly as humans do. The input text is converted into smaller units called **tokens**.

For example, a sentence such as:

```text
How do I reset my password?
```

is converted into a sequence of tokens that the model can process. Tokens can represent complete words, parts of words, punctuation or other pieces of text depending on the tokenizer. 

After tokenization, the input reaches the **LLM processing** stage. The model processes the token sequence and uses the information available in the context to determine what response to generate. At a high level, an autoregressive language model predicts the next token based on the preceding tokens and the information available in its context. This process is repeated until the model produces the generated response. The final stage is **response generation**. The LLM generates the output and the system delivers the response back to the user.

The complete lifecycle can therefore be represented as:

```text
User Input
    ↓
Prompt Reception
    ↓
Context Assembly
    ↓
Tokenization
    ↓
LLM Processing
    ↓
Response Generation
    ↓
Assistant Response
```

This process is important because the final response depends on what information enters the model during the earlier stages. For example, if the application includes conversation history or retrieved documents during context assembly, that information can influence the model's output. This also introduces important security considerations.

Any information that enters the context can potentially influence the model's behavior. If untrusted content is included in the context, such as malicious user input or a compromised external document, that content may influence the model's response. This is one of the fundamental ideas behind **prompt injection** and **indirect prompt injection**. Understanding the prompt lifecycle therefore helps us understand where attacks can enter an LLM application and how untrusted input can eventually influence model behavior.
