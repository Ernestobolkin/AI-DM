# AI-DM Engine — Data Flow

```mermaid
flowchart LR

    Player["Player Input"]
    Parser["Intent Parser"]
    Rules["Rules Engine<br>(5e mechanics)"]
    State["State Update"]
    RAG["RAG Retrieval"]
    Langflow["Langflow Pipeline"]
    LLM["Local LLM (Ollama)"]
    UI["UI Renderer"]

    Player --> Parser
    Parser --> Rules
    Rules --> State
    State --> UI

    State --> RAG
    RAG --> Langflow
    Langflow --> LLM
    LLM --> Langflow
    Langflow --> UI
