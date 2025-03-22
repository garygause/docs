# LangChain

Version: 0.3

LangChain is a framework for building "chains" of actions across LLMs, other tools, and other parts of your application.

It is a rapidly evolving library and the documentation is not always up to date.

This cheatsheet and others like it attempt to provide a quick reference for the most common tasks and patterns using a specific version of the library. Others will be added as new versions are released and time allows.

## Major Changes in v0.3

Reference: [LangChain 0.3](https://python.langchain.com/docs/versions/v0_3/)

- Pydantic 1 is no longer supported in favor of Pydantic 2.
- Python 3.8 is no longer supported in favor of Python 3.10 and above.
- `langchain.llms` is now `langchain.llms.base`
- `langchain.agents` is now `langchain.agents.base`
- Output parsers are now in `langchain_core.output_parsers`

## Installation

```bash
pip install langchain
```

#

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

Output parsers are classes in Langchain that help structure the text responses from language models into more useful formats, allowing you to convert the text into JSON, Python data classes, database rows, and more.

In v0.3, the output parser concept was integrated into the langchain_core library.

```python
from langchain_core.output_parsers import JsonOutputParser
```

## Agents

Reference: [LangChain Agents](https://python.langchain.com/docs/tutorials/agents/)
