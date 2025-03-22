# LangChain

Version: 0.2
Reference: [LangChain 0.2](https://python.langchain.com/docs/versions/v0_2/)

LangChain is a framework for building "chains" of actions across LLMs, other tools, and other parts of your application.

This document covers v0.2 of LangChain. This is not the recommended version. It is provided for reference only as you will still see it in the wild and it can be difficult to understand why some code is written the way it is. It's usually because the code was written for an older version of LangChain.

## Installation

```bash
pip install langchain
```

## Prompt Templates

Prompt templates are a reusable way to create LLM prompts. There are two types of prompt templates:

- `PromptTemplate`: A prompt template that can be used to create a prompt.
- `ChatPromptTemplate`: A prompt template that can be used to create a chat prompt.

PromptTemplates example:

```python
from langchain.prompts import PromptTemplate

prompt = PromptTemplate(
    input_variables=["product"],
    template="What is the price of {product}?",
)
```

ChatPromptTemplates example:

```python
from langchain.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate.from_template("What is the price of {product}?")
```

## Output Parsers

Reference: [Output Parsers]()
