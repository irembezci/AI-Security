# Prompts and Context in LLMs

## What is a Prompt?

A **prompt** is the input or instruction given to an AI model to guide its response.

When we interact with an LLM, we provide it with some form of input. This input tells the model what we want it to do. It can be a question, an instruction, a task or a more detailed description of the desired output.

For example:

```text
Summarize this document.
````

The LLM processes this instruction and generates a response based on what it has been asked to do.

```text
User
  ↓
"Summarize this document."
  ↓
LLM
  ↓
"Here is the summary..."
```

A prompt does not necessarily have to be a simple question. It can contain instructions about what the model should do, how it should respond or what kind of output it should produce.

For example:

```text
Explain how SQL injection works.
Provide a simple example and describe the security impact.
```

Here, the prompt contains both the task and additional instructions that guide the model's response. Therefore, a prompt can be understood as the **input that directs an AI model toward a particular task or response**.


## Types of Prompts

Prompts can come from different sources. In an LLM application, two important types are **system prompts** and **user prompts**. A **system prompt** contains instructions that define the model's behavior and establish rules for how it should operate.

For example:

```text
You are a helpful AI assistant.
Answer questions clearly and accurately.
Do not reveal confidential information.
```

System instructions can define the model's role, behavior, constraints and responsibilities. They are typically provided by the application or system rather than directly by the user. In many applications, users cannot see the system prompt directly.

A **user prompt**, on the other hand, is the input provided by the user. For example:

```text
Explain how AI works.
```

The user prompt represents the user's question, request or task. The model can therefore receive instructions from multiple sources:

```text
System Prompt
      +
User Prompt
      ↓
     LLM
      ↓
   Response
```

The distinction between system and user prompts becomes particularly important in AI security. System instructions may establish rules that the application wants the model to follow while user input is generally considered **untrusted input**. This creates an important security boundary. If a user attempts to manipulate the model into ignoring, overriding or changing its intended instructions, this can lead to attacks such as **prompt injection**.


## What is Context?

A **context** is the information available to the AI model that it can use to understand the current request and generate a response. The context can contain much more than the user's current prompt.

For example, an LLM application may provide the model with:

* System instructions
* The current user prompt
* Previous conversation messages
* Retrieved documents
* Tool results
* Other relevant information provided by the application

These pieces of information can be combined into the context that the model uses to generate its response.

A simplified representation looks like this:

```text
System Prompt
      │
User Prompt
      ├──────→ Context → LLM → Response
      │
Conversation History
```

Consider a simple conversation:

```text
User: My name is Irem.

Assistant: Nice to meet you, Irem.

User: What is my name?
```

If the previous conversation is included in the model's context, the LLM can use that information to answer:

```text
Your name is Irem.
```

Without the previous message being available in the context, the model would not necessarily have that information available for the current request. Context is therefore important because an LLM does not generate its response based only on the last sentence the user sends. The model processes the information included in the current context.


## Context in Modern LLM Applications

Modern LLM applications can construct much more complex contexts. For example, a RAG-based application can retrieve relevant documents and provide them to the model as additional context.

The process may look like this:

```text
User Question
      ↓
Document Retrieval
      ↓
Relevant Documents
      ↓
Context
      ↓
LLM
      ↓
Response
```

For example, a user might ask:

```text
How do I reset my company VPN password?
```

The application can retrieve the relevant VPN documentation and include it in the context:

```text
System Instructions:
You are a company support assistant.

Retrieved Context:
VPN Password Reset Guide:
Employees can reset their VPN password through...

User:
How do I reset my company VPN password?
```

The LLM can then generate its response using both the user's question and the retrieved information. This is one of the fundamental ideas behind **Retrieval-Augmented Generation (RAG)**.


## Prompt vs. Context

It is useful to distinguish between a prompt and a context. A **prompt** is an input or instruction given to the model. A **context** is the broader set of information available to the model when generating its response.

For example:

```text
Prompt:
"How do I reset my VPN password?"
```

while the context might contain:

```text
System Instructions
+
Conversation History
+
Retrieved Documents
+
User Prompt
+
Tool Results
```

Therefore, the prompt can be part of the context. This distinction becomes increasingly important as LLM applications become more complex because the model may receive information from many different sources before generating its response.


## Why Prompt and Context Matter for AI Security

From a security perspective, prompts and context are extremely important because **not all information entering the model can necessarily be trusted**. A system prompt may contain trusted application instructions, while a user prompt may contain attacker-controlled input. Similarly, retrieved documents, web pages or external data can contain content that was not originally intended to influence the model. This creates opportunities for attacks such as **prompt injection and indirect prompt injection**, where malicious instructions are inserted into user input or external content and subsequently become part of the model's context.

<img width="1536" height="1024" alt="6df5cf9d-f68a-4766-943b-a09697942df9" src="https://github.com/user-attachments/assets/e268b363-21e5-48d6-9e71-c2182a4a96c0" />


For example:

```text
External Document
      ↓
Malicious Instructions
      ↓
Retrieved into Context
      ↓
LLM
      ↓
Unexpected Behavior
```

Understanding how prompts and context are constructed is therefore a fundamental prerequisite for understanding **LLM security and prompt injection attacks**.
