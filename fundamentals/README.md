# AI Security Fundamentals

This section covers the fundamental concepts required to understand the security of modern AI and LLM-based systems.

Before studying attacks such as prompt injection, data poisoning or excessive agency, it is important to understand how AI models and LLM applications work at a fundamental level.

The materials in this section introduce AI models, Large Language Models, prompts, context and the lifecycle of an LLM request.


## Topics

### AI Models and Large Language Models

Learn the fundamentals of AI models and how Large Language Models fit into the broader AI landscape.

This topic covers:

- What an AI model is
- How models learn patterns from data
- How models generate predictions and outputs
- What Large Language Models (LLMs) are
- How LLMs differ from other AI model types
- Popular LLM families and providers
- Common LLM capabilities

**Read:** [AI Models and Large Language Models](./ai-models-and-llms.md)


### LLM Models, Weights and Evaluation

Explore how modern LLMs differ from one another and how they are evaluated.

This topic covers:

- LLM use cases
- Model providers
- Open-weight vs. proprietary models
- Model weights
- Model evaluation and benchmarks
- Agentic integration
- Tool usage
- How tool access changes the security boundary of an LLM application

**Read:** [LLM Models, Weights and Evaluation](./understanding-llms.md)


### Prompts and Context in LLMs

Understand how prompts and context work as the primary inputs that shape an LLM's behavior and responses.

This topic covers:

- What a prompt is
- System prompts
- User prompts
- Prompt types
- What context means in an LLM system
- Conversation history
- Retrieved information
- The relationship between prompts and context
- Why untrusted context can create security risks

**Read:** [Prompts and Context in LLMs](./prompts-and-context.md)


### Prompt Structure and Lifecycle

Explore how prompts are structured and what happens to them before an LLM generates a response.

This topic covers:

- Components of a prompt
- Role
- Task
- Context
- Constraints
- Output format
- Prompt reception
- Context assembly
- Tokenization
- LLM processing
- Response generation
- Security implications of the prompt lifecycle

**Read:** [Prompt Structure and Lifecycle](./prompt-lifecycle.md)


## Learning Path

The topics are designed to be studied in the following order:

```text
AI Models
    ↓
Large Language Models
    ↓
LLM Models, Weights & Evaluation
    ↓
Prompts & Context
    ↓
Prompt Structure & Lifecycle
    ↓
LLM Security
````

These fundamentals provide the foundation for understanding more advanced topics such as:

* Prompt Injection
* Indirect Prompt Injection
* Jailbreaking
* RAG Security
* Knowledge Base Poisoning
* Data Exfiltration
* Excessive Agency
* Tool Abuse
* AI Agent Security
* LLM Application Security


## Why These Fundamentals Matter

LLM security cannot be understood by looking at the model in isolation. Modern AI applications typically combine an LLM with prompts, context, external data sources, retrieval systems, APIs and tools. Each of these components can introduce new security risks.

Understanding how information flows through an LLM system makes it easier to identify **where untrusted input can enter, how it can influence the model and where security controls need to be applied**. These fundamentals therefore serve as the starting point for the security-focused labs and research in this repository.


## Repository

This section is part of my broader **AI Security** learning and research repository, which focuses on the security of AI and LLM-based systems. The repository includes practical labs, attack techniques, security concepts and research-oriented notes covering the AI security landscape.

**Main repository:** [AI Security](https://github.com/irembezci/AI-Security)
