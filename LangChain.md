# LangChain

Version: 0.3

LangChain is a framework for building "chains" of actions across LLMs, other tools, and other parts of your application.

It is a rapidly evolving library and the documentation is not always up to date.

This cheatsheet and others like it attempt to provide a quick reference for the most common tasks and patterns using a specific version of the library. Others will be added as new versions are released and time allows.

## Major Changes in 0.3

Reference: [LangChain 0.3](https://python.langchain.com/docs/versions/v0_3/)

- Pydantic 1 is no longer supported in favor of Pydantic 2.
- Python 3.8 is no longer supported in favor of Python 3.10 and above.
- `langchain.llms` is now `langchain.llms.base`
- `langchain.agents` is now `langchain.agents.base`

## Installation

```bash
pip install langchain
```

## Basic Usage

```python
from langchain.llms import OpenAI
```
