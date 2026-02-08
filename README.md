# my-todo-app-update

**Name:** Yuzhang Mei  
**UMID:** 94005990

This is the feature update of the todo app, a Jac client-side application with React support. The updated app supports natural language todo creation. Instead of rigid names of to-do items in the input box, users can now input a single natural-language sentence describing multiple tasks, and the system will automatically parse it into multiple individual todo items using an LLM. This improves usability by reducing friction when creating multiple related tasks.

---

## Project Structure

```
my-todo-app/
├── jac.toml                  # Project configuration
├── main.jac                  # Main application entry
├── components/               # Reusable components
│   └── AuthForm.cl.jac       # Login/signup form
│   └── IngredientItem.cl.jac # Single ingredient display
│   └── TodoItem.cl.jac       # Single todo display
├── assets/                   # Static assets (images, fonts, etc.)
└── build/                    # Build output (generated)
```

## Getting Started

1. Clone the repository.

```bash
git clone https://github.com/YuzhangMei/jac-my-todo-app-creative
cd jac-my-todo-app-creative
```

2. Start the Jaseci server

```bash
export GEMINI_API_KEY="your-key"
jac start main.jac
```

> ## Note  
> You may also use other large language models apart from Gemini if you possess their APIs.
>
> ### Alternative: Claude
> You may also choose to use Claude for AI part. To switch models, simply change the `model_name` parameter:
>```jac
>glob llm = Model(model_name="claude-sonnet-4-20250514");
>```
>However, please be aware that Anthropic API keys are **not free** — if you use Claude models, you'll need to top up your API usage balance at https://console.anthropic.com
>
> ### Supported LLM Providers
> You can use any LLM provider -- by LLM’s Model wraps LiteLLM, which supports OpenAI, Anthropic, Google, Azure, AWS Bedrock and many others. Just ensure you have the appropriate API key set up and use the model name as specified in the LiteLLM provider documentation.
> ### Self-hosted Models
> You can also host your own models locally using Ollama or serve Hugging Face models directly. For example, with Ollama:
> ```jac
> glob llm = Model(model_name="ollama/llama3.2:1b");
> ```
> This keeps everything running on your machine at no cost -- no API keys needed.

3. Open the application in your browser at http://localhost:8000 .

4. Register a new user or log in with an existing account.


## Implementation Details
- `main.jac`
    - Add LLM function declaration `split_todos`: Given an input sentence, extract and split todo items.
    - New walker `AddTodosFromText`: Add todo items based on the list of todos returned by `split_todos`.
- `frontend.cl.jac`
    - Import `AddTodosFromText` from the server
- `frontend.impl.jac`
    - Rewrite `app.addTodo`: Instead of a single todo item, use a **for loop** to include all todo items as a response to the input.

## Summary
This extension demonstrates how LLMs can be integrated into a Jac-based application to enhance user experience while maintaining clean separation between AI logic, data modeling, and UI behavior.