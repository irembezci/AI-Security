# Core Components of Modern AI

Modern AI applications are rarely limited to an LLM alone. While the language model provides the core reasoning and generation capability, real-world applications often extend its capabilities through additional components such as **RAG, memory, tools and standardized protocols such as MCP**.

These components allow an LLM to access external information, retain relevant information across interactions, interact with external systems and perform actions beyond generating text. As these capabilities are added, the application becomes more powerful but also introduces additional security boundaries and attack surfaces.

## RAG

**Retrieval-Augmented Generation (RAG)** is an architecture that allows an LLM to retrieve relevant information from external sources before generating a response.

Instead of relying entirely on the knowledge encoded in the model's parameters, the application can retrieve information from a knowledge base and include that information in the model's context.

A simplified RAG workflow looks like this:

```text
User Question
      ↓
Retriever
      ↓
Knowledge Base
      ↓
Relevant Information
      ↓
LLM Context
      ↓
Generated Response
````

For example, an organization may build an internal AI assistant that answers questions about company policies. Rather than expecting the LLM to already know the organization's internal documentation, the application can retrieve the relevant policy documents and provide them to the model as context.

This allows the system to work with information that may be specific to an organization, frequently updated or unavailable in the model's original training data.

RAG can also help reduce hallucinations by grounding responses in retrieved information. However, retrieval does not automatically make a system secure or accurate. If the knowledge base contains incorrect, outdated or malicious content, that information may also be introduced into the model's context.

This creates an important security consideration: **the data retrieved by the system can influence the model's behavior**.

RAG security therefore involves areas such as document poisoning, retrieval manipulation, indirect prompt injection and unauthorized access to sensitive information.

## Memory

**Memory** allows an AI application to retain relevant information and use it in future interactions.

Unlike the immediate context of a single request, memory is typically implemented as a mechanism outside the model itself. The application can store selected information and retrieve it later when it becomes relevant.

For example:

```text
User:
I prefer Python for backend development.

        ↓

Application Memory

"User prefers Python"

        ↓

Future Interaction

User:
What framework should I use?

        ↓

LLM

"I'd recommend Django or FastAPI..."
```

The important distinction is that storing information in memory does not mean that the LLM itself has been retrained. The information is typically stored by the surrounding application and later inserted into the context of a future request.

Memory can be implemented in different ways, including conversation history, structured user profiles, databases or vector-based storage systems.

Memory introduces additional security considerations because stored information may contain sensitive or private data. An application must therefore consider issues such as unauthorized access, excessive retention, data leakage and malicious manipulation of stored information.

Memory can also influence future model behavior. If an attacker is able to manipulate information that is stored and later retrieved as memory, that information may affect subsequent interactions.

## Tools

**Tools** allow an LLM application to interact with external systems and perform actions beyond generating text.

Without tools, an LLM can primarily generate or transform information. With tools, the application can allow the model to interact with APIs, databases, search engines, code execution environments and other external services.

For example, consider a weather assistant:

```text
User
"What is the weather in Paris?"

        ↓

LLM

        ↓

Tool Call
"weather_api(city='Paris')"

        ↓

Weather API

        ↓

Tool Result
"27°C"

        ↓

LLM

        ↓

"The current temperature in Paris is around 27°C."
```

The LLM does not necessarily know the current weather itself. Instead, it determines that an external tool is required, constructs a tool call and uses the returned information to generate the final response.

Tool use significantly expands the capabilities of an AI system because the model can now interact with external resources.

At the same time, this creates a much larger security boundary. A text-only model may produce an incorrect answer, but a model connected to tools may potentially **read data, modify records, execute operations or trigger external actions**.

This is particularly important in AI security because excessive permissions, insufficient authorization and unsafe tool design can allow manipulated model inputs to result in unintended actions.

## MCP

**Model Context Protocol (MCP)** is a standardized protocol designed to allow AI applications to communicate with external tools and services.

Instead of building a separate integration mechanism for every individual AI application and tool, MCP provides a standardized way for an AI system to discover and interact with external capabilities.

A simplified architecture looks like this:

```text
User
  ↓
AI Assistant
  ↓
MCP Client
  ↓
MCP Server
  ↓
External Tools / Services
```

The **MCP client** is part of the AI application and communicates with MCP servers. An **MCP server** exposes capabilities such as tools, resources or other contextual information to the client.

For example, an AI assistant could interact with external services such as a calendar, database or other application through an MCP server.

Conceptually:

```text
AI Assistant
      ↓
MCP Client
      ↓
MCP Server
      ↓
┌──────────┬──────────┬──────────┐
│ Calendar │ Database │  Search  │
└──────────┴──────────┴──────────┘
```

MCP therefore provides an interoperability layer between AI applications and external capabilities.

From a security perspective, this is particularly important because MCP can connect an LLM-based application to systems that contain sensitive information or have the ability to perform real-world actions.

Security considerations therefore include authentication, authorization, input validation, tool permissions, trust boundaries and the handling of untrusted content returned by external services.

## How These Components Work Together

In a modern AI application, these components do not necessarily operate independently. They can be combined to create an AI system capable of retrieving information, remembering relevant data and interacting with external systems.

A simplified architecture can look like this:

```text
                         ┌──────────────┐
                         │   Knowledge  │
                         │     Base     │
                         └──────┬───────┘
                                │
                                ↓
User → AI Application → Retriever → Context
            │                      │
            │                      ↓
            │                     LLM
            │                      │
            ├── Memory ────────────┤
            │                      │
            │                      ↓
            │                  Tool Calls
            │                      │
            ↓                      ↓
       MCP Client ─────────→ MCP Server
                                   │
                                   ↓
                            External Services
```

The LLM remains the central generation and reasoning component, but the surrounding architecture determines what information the model can access and what actions the application can perform.

This distinction is critical for AI security.

An attacker does not necessarily need to compromise the underlying model itself. Instead, they may target the components surrounding the model. Malicious content can enter through retrieved documents, manipulated memory, user prompts or external tool results. If the application gives the model access to powerful tools, manipulated input may potentially influence actions performed against external systems.

This means that the security of an AI application depends not only on the security of the LLM, but also on the security of the **data sources, context, memory systems, retrieval mechanisms, tools and integrations surrounding it**.

Understanding these components provides the foundation for analyzing the attack surface of modern AI systems.
