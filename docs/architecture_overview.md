# AI-DM Engine — Architecture Overview

```mermaid
flowchart TD

    subgraph UI["UI (Web / VTT / Discord)"]
        ChatUI["Chat + Narration"]
        MapUI["Map / Fog"]
        SheetUI["Character Sheets"]
    end

    subgraph Backend["Game API (Rules Engine)"]
        Rules["5e SRD Rules Module"]
        State["Game State Manager"]
        Parser["Intent Parser"]
        Turn["Turn Orchestrator"]
    end

    subgraph Storage["Storage Layer"]
        PG[(Postgres)]
        Vec[(Vector DB)]
    end

    subgraph LLM["AI Layer"]
        Langflow["Langflow"]
        Ollama["Ollama"]
        HF["HuggingFace (optional)"]
    end

    ChatUI --> Backend
    MapUI --> Backend
    SheetUI --> Backend

    Backend --> PG
    Backend --> Vec
    Backend --> Langflow

    Langflow --> Ollama
    Langflow --> HF
    Langflow --> Backend
