# Inside an LLM

To understand how an LLM produces a response, we need to look at what happens inside the model after a prompt is received. An LLM does not process text in exactly the same way humans do. Before the model can generate a response, the input is converted into tokens, placed within a context window and processed by the model. The model then generates the response through an inference process, where it predicts tokens one at a time.

Several concepts are important for understanding this process, including **tokens, context windows, inference and temperature**. Understanding these concepts also helps explain why LLMs can sometimes produce incorrect information or behave unpredictably.

## What are Tokens?

A **token** is a small unit of text that an LLM processes. When we provide text to an LLM, the model does not directly process the raw text as a sequence of complete words. Instead, a tokenizer converts the input into tokens.

For example:

```text
The server is running.
````

may be divided into tokens such as:

```text
The
server
is
running
.
```

The exact tokenization depends on the tokenizer and the model. A token does not necessarily correspond to a complete word. It can represent a whole word, part of a word, punctuation or another piece of text.

The general process looks like this:

```text
Input Text
    ↓
Tokenizer
    ↓
Tokens
    ↓
LLM
    ↓
Generated Tokens
    ↓
Readable Text
```

The LLM therefore processes **tokens rather than raw text**. Tokens are important because many properties of an LLM are measured in terms of tokens. For example, context window size, input length and output limits are commonly expressed using token counts.

## What is a Context Window?

A **context window** is the maximum amount of tokenized information an LLM can process as part of a single request.

The context provided to an LLM can contain many different types of information:

```text
System Instructions
+
User Prompt
+
Conversation History
+
Retrieved Documents
+
Tool Results
+
Other Application Data
```

All of this information consumes space within the available context window.

For example, imagine an LLM has a limited context capacity:

```text
┌──────────────────────────────────────┐
│           Context Window             │
│                                      │
│ System Instructions                  │
│ Conversation History                 │
│ Retrieved Documents                  │
│ Current User Prompt                  │
│                                      │
│ Remaining Capacity                   │
└──────────────────────────────────────┘
```

As more information is added, less capacity remains available for additional input and generated output. If the context becomes too large, the application or model may need to manage the available space. Depending on the implementation, older messages or other information may be truncated, removed or excluded from the request.

For example:

```text
New Information
      ↓
Context Window
      ↓
Capacity is exceeded
      ↓
Older Information May Be Removed
```

This is why context management is important in long conversations, large document-processing systems and RAG applications.

It is also important to distinguish the **context window** from the model's learned knowledge. The model's learned knowledge is encoded in its parameters as a result of training. The context window, on the other hand, contains the information that is explicitly provided to the model for the current inference request. A model can therefore have knowledge represented in its parameters without that information appearing explicitly in the current context.

## Inference

**Inference** is the process through which an LLM uses its learned parameters and the current input context to generate an output. During inference, the model predicts what token should come next based on the tokens that have already been provided or generated.

For example:

```text
Input:

What is artificial intelligence?

↓

Model generates:

Artificial

↓

Artificial intelligence

↓

Artificial intelligence is

↓

Artificial intelligence is the

↓

Artificial intelligence is the simulation...
```

The model generates the response **one token at a time**.

At a high level:

```text
Context
   ↓
LLM
   ↓
Predict next token
   ↓
Add token to sequence
   ↓
Predict next token
   ↓
Add token to sequence
   ↓
...
   ↓
Final response
```

This process is commonly described as **autoregressive generation** for models that generate text by repeatedly predicting the next token from the preceding sequence.

The important point is that the model is not simply retrieving a complete pre-written answer from a database. Instead, it uses its learned parameters and the current context to calculate a probability distribution over possible next tokens and then selects a token according to the configured decoding strategy. The selected token becomes part of the sequence and influences the prediction of the next token.

## Temperature

**Temperature** is a parameter that affects how the probability distribution is used when selecting the next token during generation. A lower temperature generally makes the model's token selection more concentrated around higher-probability tokens. This tends to produce more predictable and consistent responses.

A higher temperature generally makes the distribution less concentrated, allowing lower-probability tokens to have a greater chance of being selected. This can produce more varied and creative responses.

Conceptually:

```text
Lower Temperature
        ↓
More predictable
More consistent
More focused
```

while:

```text
Higher Temperature
        ↓
More diverse
More variable
Less predictable
```

For example, consider the prompt:

```text
Write a short description of a sunset.
```

With a lower temperature, repeated generations may produce relatively similar responses. With a higher temperature, the model may produce more varied wording and different descriptions.

It is important to understand that temperature does **not retrain or modify the model**. It affects the decoding or sampling process used during generation.

Temperature is therefore useful when an application needs to balance **determinism and diversity**. For tasks such as structured extraction, classification or generating predictable formats, lower randomness may be preferred. For creative writing or brainstorming, more variation may be desirable.

## Hallucination

One of the most important limitations of LLMs is **hallucination**. A hallucination occurs when an LLM generates information that is incorrect, fabricated or unsupported while presenting it as if it were accurate.

For example:

```text
User:
Who wrote the novel "The Silent Planet"?

LLM:
The novel was written by John Smith in 1998.
```

If the book or author does not actually exist, the model has fabricated information rather than providing a verified fact. The important issue is that the response can still appear fluent and confident.

This happens because an LLM is fundamentally a probabilistic language generation system. During generation, it predicts likely token sequences based on its learned parameters and the available context. The model does not inherently guarantee that every generated statement is factually correct or externally verified.

A simplified representation is:

```text
Prompt
  ↓
Context
  ↓
LLM
  ↓
Token Prediction
  ↓
Generated Response
  ↓
Potentially Incorrect Information
```

Hallucinations can occur for different reasons, including insufficient context, ambiguous questions, gaps in the model's learned information or the generation of plausible-sounding content without reliable grounding.

This is one reason why modern AI applications often use techniques such as **RAG, tool calling, external knowledge sources and validation mechanisms** to improve factual reliability.

For example:

```text
User Question
      ↓
Retrieve Relevant Information
      ↓
Context
      ↓
LLM
      ↓
Grounded Response
```

However, adding external information does not automatically eliminate hallucinations. The retrieved information must be relevant and trustworthy, and the application must correctly control how the model uses that information.

## Putting the Concepts Together

These concepts are closely connected. When a user submits a prompt, the application constructs the context and converts the input into tokens. These tokens, together with any other information included in the request, occupy the model's context window. The LLM then processes this context during inference and predicts the response one token at a time. The decoding process can be influenced by parameters such as temperature.

The complete flow can be simplified as:

```text
User Prompt
     ↓
Context Assembly
     ↓
Tokenization
     ↓
Context Window
     ↓
LLM Inference
     ↓
Next-Token Prediction
     ↓
Sampling / Decoding
     ↓
Generated Tokens
     ↓
Readable Response
```

This process explains several important characteristics of LLMs. The model operates on **tokens**, not raw text. The **context window** determines how much tokenized information can be processed in a request. During **inference**, the model generates a response through sequential token prediction. **Temperature** can influence how deterministic or variable the generation is. Because the model does not inherently verify every generated statement against an external source, it can produce **hallucinations**.

Understanding these mechanisms is essential for AI security because many attacks target the information and instructions that enter this generation process. An attacker may attempt to manipulate the tokens included in the context, inject malicious instructions into retrieved content, influence the model's interpretation of existing instructions or exploit the way an application passes information to the model.

These concepts provide the foundation for understanding attacks such as **prompt injection, indirect prompt injection, jailbreaks, RAG attacks and data exfiltration**.

