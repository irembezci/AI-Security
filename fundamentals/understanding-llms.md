# Understanding LLMs: Models, Weights, Evaluation and Tool Usage

Now that we understand what a Large Language Model is and what it can do, we can take a closer look at how LLMs differ from one another and how they are evaluated.

There are several important aspects to consider when working with LLMs. These include the **model and its use case, the provider, how the model weights are made available, how the model is evaluated and whether the model can interact with external tools**.

## 1. Models

First, we need to understand that not all LLMs are designed for exactly the same purpose. Some models are designed as general-purpose assistants while others are optimized for specific tasks such as reasoning, coding, mathematics or working with multimodal data.

<img width="1800" height="1017" alt="Screenshot 2026-09-13 at 3 34 36 AM" src="https://github.com/user-attachments/assets/b55bdf6d-3870-4bf1-8487-45a4b0c572b0" />


We can therefore categorize models based on their **use cases**. For example, a general-purpose model may be designed to handle conversations, writing and general knowledge tasks while a coding oriented model may be optimized for generating and understanding source code.

Another important aspect is the **provider**. Different organizations develop different LLM families.

For example:

- OpenAI → GPT
- Anthropic → Claude
- Google → Gemini
- Meta → Llama
- Alibaba → Qwen
- DeepSeek → DeepSeek

These models may differ in architecture, training data, capabilities, performance and deployment options. So when comparing LLMs, we should not simply ask which model is "the best." We should first ask **which model is best suited for a particular use case**.


## 2. Model Weights

Another important distinction is how the model's **weights** are made available. Model weights are the learned numerical parameters that represent what the model has learned during training. They are a fundamental part of the trained model.

There are two broad categories we commonly encounter: **open-weight models** and **proprietary or closed-weight models**.

With an **open-weight model**, the trained weights are made available to users or developers. This can allow them to download the model, run it on their own infrastructure and potentially fine-tune or modify it, depending on the model's license. Examples include model families such as Llama, Qwen and Mistral.

With a **proprietary or closed-weight model**, the model's weights are not provided to the user. Instead, users typically interact with the model through a hosted service or an API.

For example:

```text
Your Application
       ↓
      API
       ↓
   LLM Provider
       ↓
   Model
       ↓
    Response
````

You can send prompts to the model and receive responses but you do not have direct access to the model's internal weights. This distinction is important from a security perspective because it affects **where the model runs, who controls the infrastructure, who can access the weights and how much control the organization has over the model**.


## 3. Model Evaluation

The next question is: **How do we know whether one model performs better than another?** This is where **model evaluation and benchmarks** become important. An evaluation is a structured way of testing a model's capabilities. Different evaluations can measure different aspects of performance, such as reasoning, mathematics, coding, knowledge or instruction following.

For example, an evaluation might look like this:

```text
                 LLM
                  ↓
        ┌─────────┼─────────┐
        ↓         ↓         ↓
    Reasoning   Coding     Math
        ↓         ↓         ↓
        └─────────┼─────────┘
                  ↓
             Evaluation
                  ↓
              Score / Rank
```

The screenshot shows an example of this approach through **Artificial Analysis** which provides different model evaluations and leaderboards. For example, an overall intelligence index can combine multiple evaluations while other benchmarks may focus specifically on areas such as agentic tasks or analytical work.

<img width="1800" height="1017" alt="Screenshot 2026-09-13 at 3 36 34 AM" src="https://github.com/user-attachments/assets/489a9a8f-3453-4206-bdce-e47430e97bdf" />

This is why model comparisons should always be interpreted in context.

Instead of simply saying:

> "Model A is better than Model B."

we should ask:

> **"Which model performs better, on which task, according to which evaluation?"**

A model may perform extremely well on coding but not necessarily be the best choice for another task.


## 4. Agentic Integration and Tool Usage

The final concept in this walkthrough is **agentic integration**, particularly the ability of an LLM to use external tools. A basic LLM receives an input and generates an output. However, an LLM integrated with tools can interact with external systems to perform actions or retrieve information.

For example, imagine a user asks:

```text
What is the current status of my flight?
```

Instead of relying only on its internal knowledge, the LLM can call a flight-status API:

```text
User
 ↓
LLM
 ↓
Tool / API
 ↓
Flight System
 ↓
Flight Status
 ↓
LLM
 ↓
User
```

The model determines that it needs external information, calls the appropriate tool, receives the result and then uses that result to generate a response.

Tools can provide access to many different capabilities, such as:

* APIs
* Databases
* Search engines
* File systems
* Calculators
* Enterprise applications

This changes the security model significantly. An LLM that can only generate text has a relatively limited ability to affect the outside world. An LLM that can call APIs, access databases or perform actions has **agency**. This is why tool usage becomes particularly important when we later discuss **AI agents, excessive agency, tool security and LLM application security**.


## Key Takeaway

At this point, we can look at an LLM from four different perspectives:

```text
LLM
 │
 ├── Models
 │    ├── Use Cases
 │    └── Providers
 │
 ├── Weights
 │    ├── Open-weight
 │    └── Proprietary / Closed-weight
 │
 ├── Evaluation
 │    └── Benchmarks & Leaderboards
 │
 └── Agentic Integration
      └── Tool Usage
```

Understanding these concepts gives us a better picture of what an LLM actually is, how different models can be compared and how LLMs can become part of larger AI systems. This is particularly important for security because the **model itself is only one part of the attack surface**. Once an LLM is connected to external data, APIs, tools or other systems, additional security risks can emerge.

