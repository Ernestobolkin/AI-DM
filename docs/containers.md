# AI-DM Engine — C4 Container Diagram

```mermaid
C4Container
title AI-DM D&D Engine - Containers

Boundary(api_b, "Game Backend"){
  Container(api, "Game API", "FastAPI / NestJS", "Deterministic rules, state, WebSockets")
  ContainerDb(pg, "Postgres", "SRD mechanics + player state")
  ContainerDb(vec, "Vector Store", "pgvector / Chroma / Qdrant")
}

Container(ui, "UI", "Next.js / Web", "Chat, map, sheets, dice, combat UI")
Container(langflow, "Langflow", "LLM Orchestration", "RAG, prompt pipelines, JSON validation")
Container(ollama, "LLM Runtime", "Ollama (local models)", "Llama3-8B, Mistral-7B")
Container_Ext(hf, "HF Inference API", "HuggingFace", "Optional external LLM inference")

Rel(ui, api, "Actions / Turns / Realtime", "WebSocket / REST")
Rel(api, pg, "Read/write rules + state", "SQL")
Rel(api, vec, "Embed / Retrieve", "HTTP / local")
Rel(api, langflow, "Narration / Dialogue Requests")
Rel(langflow, ollama, "Prompt → Response", "OpenAI-compatible API")
Rel(langflow, hf, "Optional inference")
Rel_Back(langflow, api, "JSON: narration, npc_lines, options")
