# Chat Completions API

## Learning Goals
- Learn how to use the Chat Completions API.
- Understand the key parameters and response of the API.
- Use a command-line interface (CLI) to interact with the API.

## Introduction
This project demonstrates how to interact with OpenAI's Chat Completion API, the latest API for models like GPT-4. You will learn how to create functions to send prompts and manage chat conversations, while understanding the key parameters involved in the API call.

## Setup
1. Clone the repository.
2. Install dependencies using Pipenv:
   ```bash
   pipenv install
   ```
3. Create a `.env` file with your OpenAI API key:
   ```bash
   OPENAI_API_KEY=your-api-key-here
   ```

## Basic Prompt Function

This function sends a single prompt to the API and returns the assistant's response.

### Code:
```python
def get_completion(prompt, model="gpt-3.5-turbo", temperature=0):
    messages = [{"role": "user", "content": prompt}]
    
    response = openai.ChatCompletion.create(
        model=model,
        messages=messages,
        temperature=temperature,
    )
    
    return response.choices[0].message["content"]
```

### Usage:
```python
prompt = "What is the capital of New York?"
print(get_completion(prompt))
```

### Key Parameters:
- `model`: Specifies which OpenAI model to use (default is `gpt-3.5-turbo`).
- `messages`: A list of conversation messages, including the user input.
- `temperature`: Controls the randomness of the response (0.0 to 1.0).

## Context-Aware Function

This function tracks the conversation history between the user and the assistant, allowing for context-aware interactions.

### Code:
```python
def get_completion_from_messages(messages, model="gpt-3.5-turbo", temperature=0):
    response = openai.ChatCompletion.create(
        model=model,
        messages=messages,
        temperature=temperature,
    )
    return response.choices[0].message["content"]
```

### Example Usage:
```python
messages = [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Who won the world series in 2020?"},
    {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
    {"role": "user", "content": "Where was it played?"}
]

print(get_completion_from_messages(messages))
```

## CLI Integration
You can integrate these functions with a command-line interface (CLI) for user interaction. 

### Example in `app.py`:
```python
from ai import get_completion

prompt = input('Enter prompt: ')
response = get_completion(prompt)
print(response)
```

### Running the App:
```bash
pipenv run python app.py
```

## API Response Structure

The response from the Chat Completion API typically contains:
- `choices`: Contains the generated response(s).
- `usage`: Displays the number of tokens used in the request.

### Example Response:
```json
{
  "id": "chatcmpl-7aoO5OF9Cq4Mo3mrYXtNg9ddQjVQr",
  "model": "gpt-3.5-turbo",
  "choices": [
    {
      "message": {
        "role": "assistant",
        "content": "The capital of New York is Albany."
      }
    }
  ],
  "usage": {
    "prompt_tokens": 15,
    "completion_tokens": 8,
    "total_tokens": 23
  }
}
```

## Conclusion
In this project, you’ve learned how to use OpenAI’s Chat Completions API, explored the key parameters, and integrated your functions into a CLI app. You can now build more advanced chatbots or assistants with contextual awareness.

## Resources
- [OpenAI Chat Completions API Overview](https://platform.openai.com/docs/guides/gpt/chat-completions-api)
- [API Reference](https://platform.openai.com/docs/api-reference/chat/create)
- [Messages List API Reference](https://platform.openai.com/docs/api-reference/chat/create#chat/create-messages)
- [OpenAI Libraries](https://platform.openai.com/docs/libraries)
- [GPT Best Practices](https://platform.openai.com/docs/guides/gpt-best-practices)