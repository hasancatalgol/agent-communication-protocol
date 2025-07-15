# 🧠 What is ACP (Agent Communication Protocol)?

**ACP (Agent Communication Protocol)** is an open protocol designed for building **modular, interoperable AI agents** that can communicate and collaborate through standardized HTTP APIs.

---

## 🚀 Key Concepts

### Agent = Stateless Service

- Each agent is an HTTP server that accepts input messages and returns responses.
- Agents can be LLM-backed tools, retrieval systems, function wrappers, or anything else with logic.

### Message Format

- Agents communicate using structured message objects (`role`, `content`, optional `tool_calls`, etc.).
- Compatible with LLM chat formats.

### Standard API Endpoints

Every agent implements the same REST API:

- `GET /agents` – list available agents  
- `POST /agents/<name>/run_sync` – send message and get immediate reply  
- `POST /agents/<name>/run` – for streaming or async use  

### Language-Agnostic

- ACP is not tied to any language or platform.
- Python and TypeScript SDKs are available, with others planned.

---

## 🧩 Why ACP?

- 📦 **Composable**: Easily plug agents together, no need for custom glue code.
- 🔄 **Interoperable**: Agents can talk to each other over HTTP, no shared runtime needed.
- 📐 **Minimalist**: Just JSON over REST. No special frameworks or platforms required.
- 💬 **LLM-Friendly**: Message structure maps cleanly to OpenAI/Anthropic prompt formats.

---

# 🧠 ACP Agent Server – Run & Test Guide

This project runs an [Agent Communication Protocol (ACP)](https://agentcommunicationprotocol.dev) server using Python and the `acp-sdk`.

---

## 🚀 Running the Agent Server

Start the server using [`uv`](https://github.com/astral-sh/uv):

```bash
uv run agent.py
```

Once running, the server will be available at:

```
http://localhost:8000
```

---

## 🧪 Interacting with the Agent

### 🔍 List Available Agents

```bash
curl http://localhost:8000/agents | jq
```

You should see:

```json
{
  "agents": [
    {
      "name": "echo",
      "description": "Echoes everything",
      "metadata": {
        "annotations": null,
        "documentation": null,
        "license": null,
        "programming_language": null,
        "natural_languages": null,
        "framework": null,
        "capabilities": null,
        "domains": null,
        "tags": null,
        "created_at": null,
        "updated_at": null,
        "author": null,
        "contributors": null,
        "links": null,
        "dependencies": null,
        "recommended_models": null
      },
      "input_content_types": [
        "*/*"
      ],
      "output_content_types": [
        "*/*"
      ]
    }
  ]
}
```

---

### 📤 Send a Message to the Echo Agent

```bash
curl -X POST http://localhost:8000/runs \
  -H "Content-Type: application/json" \
  -d '{
        "agent_name": "echo",
        "input": [
          {
            "role": "user",
            "parts": [
              {
                "content": "Howdy!",
                "content_type": "text/plain"
              }
            ]
          }
        ]
      }'
```

Expected output:

```json
[
  {
    "role": "agent",
    "content": "Echo: Hello from ACP"
  }
]
```

---

## 🛑 Stopping the Server

To shut down the server, press:

```
Ctrl + C
```

in your terminal.

---

## 📎 Useful Links
- 🔗 [ACP Documentation](https://agentcommunicationprotocol.dev/introduction/quickstart)
- 🧰 [acp-sdk on PyPI](https://pypi.org/project/acp-sdk/)
- 📦 [uv Package Manager](https://github.com/astral-sh/uv)