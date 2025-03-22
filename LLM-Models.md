# LLM Models

There are many LLM models in existence today. This document gives a quick overview of some of the most popular ones along with some examples of how to use them with LangChain.

Ollama

Open Source (Local):

- Mistral
- Llama3 (Meta)

First Tier (Pay):

- GPT-4 (OpenAI)
- Claude (Anthropic)
- Gemini (Google)

## Ollama

Ollama is a lightweight, fast, and easy-to-use LLM engine that can run locally. To install Ollama, follow the instructions [here](https://ollama.com/docs/installation).

You can run a model with:

```bash
ollama run llama3
```

You can pull a model with:

```bash
ollama pull llama3
```

You can list all pulled models with:

```bash
ollama list
```

You can remove a model with:

```bash
ollama remove llama3
```

Models are stored at `~/.ollama/models` on Mac and `/usr/share/ollama/.ollama/models` on Linux.

Once a model is available locally, you can use it with LangChain.

### Changing the default model directory

Various methods for changing the default model directory are listed online with limited success. This is the only method that has worked for me.

Bind the model directory to a new location.

```bash
sudo mount --bind /media/dev/ml/ollama/models /usr/share/ollama/.ollama/models
```

And update fstab:

```bash
# /etc/fstab

# ollama models
/media/dev/ml/ollama/models     /usr/share/ollama/.ollama/models     none     defaults,bind     0 0
```

Then restart the ollama service:

```bash
sudo systemctl restart ollama
sudo systemctl status ollama
```

Test the connectivity:

```bash
curl http://localhost:11434/api/version

# and

ollama list
```

### LangChain integration:

First run or pull the model with Ollama. Then install the LangChain integration:

```bash
pip install langchain-ollama
```

Then use the model in LangChain:

```python
from langchain_ollama import ChatOllama
from langchain_core.prompts import PromptTemplate
from langchain_core.output_parsers import StrOutputParser

llm = ChatOllama(model="llama3")

summary_template = """
Given the information {information} about a person from I want you to create:
1. a short summary
2. two interesting facts about them
"""

summary_prompt = PromptTemplate(
    input_variables="information", template=summary_template
)
chain = summary_prompt | llm_ollama | StrOutputParser()

result = chain.invoke(
    {
        "information": "Dr. John Doe is a 32 year old male who is 1.8 meters tall and weighs 80 kilograms. He is a doctor who studied at Harvard University and has a passion for helping people."
    }
)

print(result)
```

### References:

- [Ollama](https://ollama.com/)
- [Ollama Models](https://ollama.com/models)
- [LangChain Ollama](https://python.langchain.com/docs/integrations/chat/ollama/)

## Open Source Models

### Llama3

Reference: [Llama3](https://llama.meta.com/)

Llama3 is a family of LLM models from Meta.

Running locally with Ollama

```bash
ollama run llama3
```

LangChain example:

```python
from langchain_ollama import ChatOllama

llm = ChatOllama(model="llama3")
```

### Mistral

Reference: [Mistral](https://mistral.ai/)

Mistral is a family of LLM models from Mistral.ai.

Running locally with Ollama

```bash
ollama run mistral
```

LangChain example:

```python
from langchain_ollama import ChatOllama

llm = ChatOllama(model="mistral")
```

## First Tier Models

First Tier models are the pay-to-play models. They excel at a wide range of tasks and are required for some use cases, including reasoning and math.

They also require an API key to use.

### GPT-4 (OpenAI)

Reference: [GPT-4](https://openai.com/api/gpt-4/)

LangChain example:

Install the LangChain OpenAI integration:

```bash
pip install langchain-openai
```

Then use the model in LangChain:

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4")
```

### Claude (Anthropic)

Reference: [Claude](https://anthropic.com/claude)

LangChain example:

Install the LangChain Anthropic integration:

```bash
pip install langchain-anthropic
```

Then use the model in LangChain:

```python
from langchain_anthropic import ChatAnthropic

llm = ChatAnthropic(model="claude-3-5-sonnet")
```

### Gemini (Google)

Reference: [Gemini](https://gemini.google.com/)

LangChain example:

Install the LangChain Google Gemini integration:

```bash
pip install langchain-google-gemini
```

Then use the model in LangChain:

```python
from langchain_google_gemini import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(model="gemini-1.5-flash")
```
