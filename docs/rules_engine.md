# Rules Engine — Internal Modules

```mermaid
flowchart TD

    subgraph Char["Character Module"]
        Abilities["Abilities / Modifiers"]
        Skills["Skills / Proficiency"]
        Inventory["Inventory"]
    end

    subgraph Combat["Combat Module"]
        Initiative["Initiative Order"]
        Attack["Attack Resolution"]
        Save["Saving Throws"]
        Movement["Movement / AoO"]
        Conditions["Conditions (prone, grappled…)"]
    end

    subgraph World["World Data"]
        NPCs["NPCs"]
        Monsters["Monsters"]
        Encounters["Encounter Builder"]
        Quests["Quest Graph"]
    end

    subgraph Data["SRD Data Sources"]
        PG[(Postgres<br>mechanics)]
        Vec[(Vector DB<br>SRD text)]
    end

    Char --> Combat
    Combat --> World
    World --> Data
