## 🎞️ How the Operational Workflow Connects

![HSE Risk Intelligence operational architecture](../images/operational_architecture.gif)

---

## 🔄 Conceptual Operational Risk Model

```mermaid
flowchart TB

    subgraph F1["1 · Foundation"]
        SITE["Site<br/>Section<br/>Zone"]
        PEOPLE["People<br/>Teams<br/>Organizations"]
    end

    subgraph F2["2 · Planning & Field Operations"]
        PLAN["PWP · PTW<br/>JSA · Method Statements"]
        TOOLBOX["Toolbox<br/>& Preparedness"]
        TASK["Task<br/>Execution"]
        WEATHER["Weather<br/>& Conditions"]

        PLAN --> TASK
        TOOLBOX --> TASK
        WEATHER --> TASK
    end

    subgraph F3["3 · Risk Detection"]
        OBS["Observation"]
        HAZ["Hazard"]
        HCTRL["Hazard<br/>Controls"]

        TASK --> OBS
        TASK --> HAZ
        OBS --> HAZ
        HAZ --> HCTRL
    end

    subgraph F4["4 · Incident Response"]
        INC["Incident<br/>or Event"]
        ICTRL["Incident<br/>Controls"]

        TASK --> INC
        OBS --> INC
        INC --> ICTRL
    end

    subgraph F5["5 · Follow-Up & Assurance"]
        CA["Corrective<br/>Action"]
        VERIFY["Verification<br/>& Closure"]

        OBS --> CA
        HAZ --> CA
        HCTRL --> CA
        INC --> CA

        CA --> VERIFY
        HCTRL --> VERIFY
        ICTRL --> VERIFY
    end

    subgraph F6["6 · Confirmation & Management"]
        DRILL["Emergency<br/>Drills"]
        CONFIRM["Daily Close<br/>& Confirmation"]
        REPORT["Management<br/>Report"]
        OUTPUT["Analytics-Ready<br/>Outputs"]

        VERIFY --> CONFIRM
        DRILL --> CONFIRM
        CONFIRM --> REPORT
        REPORT --> OUTPUT
    end

    SITE --> PLAN
    SITE --> TOOLBOX
    PEOPLE --> TASK
    SITE --> DRILL
```

This is a conceptual model. The physical PostgreSQL implementation contains additional relationship, lifecycle, audit, lookup, approval, and history tables.
