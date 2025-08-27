# WebSummarization-Ollama-and-DeepSeek 
 
Overview 
--------
This repository contains an exploratory Jupyter Notebook ("Project 2 - Ollama.ipynb") that demonstrates how to call local LLM (large language model) servers (Ollama and DeepSeek) in different ways from Python. It is aimed at beginners who want to learn how to send chat-like messages to models running on a local API endpoint (typically `http://localhost:11434`) and to compare a few client approaches (raw HTTP requests, the `ollama` Python client, and an OpenAI-compatible client wrapper).

Repository structure 
--------------------
- LICENSE — MIT license covering this repo.
- Project 2 - Ollama.ipynb — interactive notebook with examples and output captured.
- README.md — (this file) high-level explanation and quick start.

What this notebook shows
------------------------
The notebook contains example code and outputs that illustrate three main approaches:

1. Method 1 — HTTP POST to Ollama API using `requests`:
   - Build a `messages` list (chat-format with `role` and `content`).
   - Send a JSON payload to `http://localhost:11434/api/chat` (or your configured Ollama endpoint).
   - Inspect response JSON and print assistant content.

2. Method 2 — Using the `ollama` Python client:
   - Call `ollama.chat(model="llama3.2", messages=messages)` to get a response.
   - This is a higher-level convenience wrapper around the service. 

3. OpenAI-compatible usage (both Ollama and DeepSeek):
   - Use an OpenAI-compatible client (the notebook uses an `OpenAI` wrapper configured with `base_url='http://localhost:11434/v1'` and a placeholder `api_key`).
   - This demonstrates interoperability: local LLM servers that speak the OpenAI API style can be used with existing OpenAI SDK patterns.
   - The notebook includes an example using `deepseek-r1:1.5b` to show swapping models.

Key files and cells
-------------------
- Import / setup cells: imports like `requests`, `BeautifulSoup` (unused for summarization demonstration but included), `urllib`, `openai`-style client, and `dotenv`.
- API configuration: variables like `OLLAMA_API = "http://localhost:11434/api/chat"` and headers.
- Message payloads: examples of how to structure prompts in chat format.
- Request/response inspection: prints HTTP status codes and `response.json()` outputs to show model content and metadata.

Quickstart (for beginners)
--------------------------
1. Install Python 3.8+ (notebook metadata shows 3.11 used).
2. Clone the repo:
   - git clone <repo-url>
   - cd WebSummarization-Ollama-and-DeepSeek

3. Create a virtual environment (recommended):
   - python -m venv .venv
   - source .venv/bin/activate  (macOS/Linux)
   - .venv\Scripts\activate     (Windows PowerShell)

4. Install required Python packages (suggested):
   - pip install jupyterlab requests beautifulsoup4 python-dotenv openai ollama
   - Note: if `ollama` package is not available via pip, the notebook shows direct HTTP usage (requests) as an alternative.

5. Run Jupyter:
   - jupyter lab  or  jupyter notebook
   - Open "Project 2 - Ollama.ipynb" and run cells sequentially.

6. Prepare & run the LLM server(s):
   - Install and run Ollama (or the local model server you plan to use). The examples expect an API at `http://localhost:11434`.
   - Ensure the model names used in the notebook (e.g., `llama3.2`, `deepseek-r1:1.5b`) are installed or available on your local server. Replace with a model name you have if necessary.

Configuration tips
------------------
- If using environment variables, create a `.env` file and load it in the notebook (the notebook imports `dotenv` but doesn't show a specific `.env`). Example entries:
  - OLLAMA_URL=http://localhost:11434
  - OLLAMA_API_KEY=<your-key-if-required>
- If the server is OpenAI-compatible, you can point an OpenAI client to the local base URL (as shown in the notebook).

Troubleshooting
---------------
- Connection refused / cannot connect:
  - Confirm the local model server (Ollama) is running and accessible at `localhost:11434`.
  - Confirm firewall or container port mappings allow access.
- Model not found:
  - Verify you have the model installed locally or change the model name to one that exists on your server.
- Python package errors:
  - Use a virtual environment and ensure you installed packages with the correct Python interpreter.

Security & privacy notes
------------------------
- Local model servers may process the prompts you send. Do not send sensitive or private data unless you understand the server configuration and storage policies.
- If you expose the API endpoint to networks, secure it appropriately (authentication, network restrictions).

Next steps & learning resources
-------------------------------
- Learn about the chat message format (role/message pairs) used by modern LLMs (system / user / assistant roles).
- Explore Ollama documentation to install models and run the local server.
- Read the OpenAI API docs to understand the OpenAI-compatible request/response formats used by many local LLM servers.
- Try modifying the `messages` in the notebook to explore prompt engineering and see how the model behaviour changes.

License
-------
This project is licensed under the MIT License. See LICENSE file.

Contact / Contribution
----------------------
This is an educational / demo notebook. Suggestions and improvements (better docs, additional examples, a requirements.txt, or a small wrapper script) are welcome — open a PR or issue in the repo.

Enjoy exploring local LLMs with Ollama and DeepSeek!
