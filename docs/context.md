# AI-DM Engine — C4 Context Diagram

```mermaid
C4Context
title AI-DM D&D Engine - Context
Person(p, "Players", "Type actions, read narration")
System_Boundary(sys, "AI-DM System"){
  System(ui, "UI (Web/Discord)", "Chat + map + sheets")
  System(api, "Game API / Engine", "Deterministic rules + state")
  SystemDb(db_mech, "Rules DB", "5e SRD mechanics (structured)")
  SystemDb(db_kb, "Text KB + Vectors", "SRD text + embeddings")
  System(langflow, "Langflow Orchestrator", "LLM chains & RAG")
  System_Ext(models, "LLM Inference", "Ollama / HF Inference")
}
Rel(p, ui, "Play session")
Rel(ui, api, "Actions / Updates")
Rel(api, db_mech, "Read/Write mechanics/state")
Rel(api, db_kb, "RAG retrieve/insert")
Rel(api, langflow, "Prompt with small context")
Rel(langflow, models, "Generate narration/dialogue")
Rel_Back(langflow, api, "JSON (narration, options, npc lines)")
