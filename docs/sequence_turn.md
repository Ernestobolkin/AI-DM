# Combat Turn — Sequence Diagram

```mermaid
sequenceDiagram
    participant P as Player
    participant UI as UI (Web)
    participant API as Game API (Rules Engine)
    participant KB as Vector Store (RAG)
    participant LF as Langflow
    participant LLM as LLM (Ollama/HF)

    P->>UI: "I sneak behind the guard."
    UI->>API: action = { type:"stealth", target:"guard-1" }

    API->>API: Resolve Stealth check (d20 + DEX + prof)
    API-->>UI: mechanic result (SUCCESS/FAIL)

    API->>KB: Retrieve lore snippets
    KB-->>API: 2–3 snippets

    API->>LF: Send scene + result + snippets
    LF->>LLM: Generate narration (JSON)
    LLM-->>LF: JSON
    LF-->>API: narration + npc_lines + options

    API-->>UI: Stream narration and update map
