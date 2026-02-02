# 📌 Conceptual Risk Intelligence Model

Below is a high-level, task-centered ERD diagram showing how risk information flows through the system. <br><br>


erDiagram
    SITE ||--o{ ZONE : contains
    ZONE ||--o{ PHASE : includes
    PHASE ||--o{ TASK : defines

    PERSON ||--o{ ATTENDANCE : logs
    ATTENDANCE }o--|| TASK : supports

    TASK ||--o{ PTW : requires
    TASK ||--o{ JSA : requires

    PERSON ||--o{ PERSON_CERTIFICATION : holds
    PTW ||--o{ PTW_CERTIFICATION : requires
    JSA ||--o{ JSA_CERTIFICATION : requires

    TASK ||--o{ INCIDENT : leads_to
    INCIDENT ||--o{ INTERVENTION : triggers
    INTERVENTION ||--o{ CORRECTIVE_ACTION : results_in

    TASK ||--o{ OBSERVATION : generates
    OBSERVATION ||--o{ CORRECTIVE_ACTION : may_create

    TASK ||--o{ HAZARD : exposes
    HAZARD ||--o{ HAZARD_CONTROL : mitigated_by
    HAZARD_CONTROL }o--|| CONTROL : uses

    HAZARD }o--|| SEVERITY_LEVELS : rated_by
    HAZARD }o--|| PROBABILITY_LEVELS : rated_by
    SEVERITY_LEVELS ||--o{ RISK_MATRIX : defines
    PROBABILITY_LEVELS ||--o{ RISK_MATRIX : defines

    HAZARD_CONTROL }o--|| CONTROL_EFFECTIVENESS_SCALE : evaluated_by

    WEATHER }o--|| TASK : influences


