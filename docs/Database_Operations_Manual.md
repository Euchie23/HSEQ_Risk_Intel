# 📒 Database Operations Manual 📒
## HSE-Q Risk Intelligence System

---

## 🔐 Data Ethics, Governance & Portfolio Use

This database design is based on field-derived HSE observations, daily safety reports, PPE verification sheets, and operational records authored during routine site oversight.

The system is **not built from any proprietary company database or internal system**.

All records (tasks, hazards, observations, incidents, toolbox topics, attendance) originate from independent HSE documentation and are structured into a relational model for analytics and portfolio demonstration.

### For Portfolio / GitHub Use

To ensure professional ethics and confidentiality:

- Worker identities are anonymized in the `PERSON` table  
- Site and company identifiers are generalized  
- PTW, JSA, and certification IDs are abstracted  
- Risk matrices are generalized into lookup tables  
- No proprietary templates or internal systems are reproduced  

### What This Dataset Represents

This is a **structured abstraction of real operational safety behavior**, preserving:

- Task → Hazard relationships  
- Observation-driven risk identification  
- Control effectiveness tracking  
- Incident escalation pathways  
- Corrective action lifecycle  
- Workforce and contractor dynamics  

👉 While maintaining full confidentiality.

---

## 1. Purpose of the System

This is **not an incident log**.

It is a **Risk Intelligence System** designed to:

- Understand risk **before work starts**
- Monitor risk **during execution**
- Learn from risk **after events occur**
- Enable **predictive and simulation-based risk analysis**

The system is anchored on:
**Site → Zone → Phase → Task → Task Execution**
with **observations** and **hazards** also able to exist independently.

> **Alignment:** NEBOSH + ISO 45001:2018 + Barrier-Based Risk Management (BP / Shell / TotalEnergies philosophy)

---

## 2. Observations Update Rule

| Column | Notes |
|--------|------|
| `observation_id` | Primary key |
| `observation_date` | Date of observation |
| `person_id` | Reporter |
| `task_execution_id` | Nullable |
| `phase_id` | Optional |
| `observation_type_id` | Classification |
| `description` | Description |
| `validated_by` | Reviewer |
| `linked_incident_id` | Optional |
| `validation_outcome` | Outcome |
| `notes` | Additional context |

👉 Observations **do not need to be task-linked** to be valid or actionable.

---

## 3. Task-Linked Records

When tasks exist, they drive:

- Attendance  
- PPE checks  
- Hazards  
- Incidents  
- Weather  
- Task-linked observations  

👉 These must reference `task_execution_id`.

---

## 4. Work Planning Before Execution

Before execution:

1. PTW issued  
2. JSA prepared  
3. Certifications verified  
4. Personnel validated  

### PTW & JSA Source Governance

Tables:
- `ptw_source_type`
- `jsa_source_type`

Rules:

- Must specify Contractor vs Client  
- Multiple records allowed per task  
- Required for audit traceability  

---

## 5. Planning Layer (Toolbox Meetings)

Toolbox meetings define **pre-task risk planning**:

- Hazards identified  
- Controls planned  
- Independent of exposure  

Tables:
- `toolbox_meeting`
- `toolbox_meeting_task`

---

## 6. Conditions & Exposure (NEW)

Tables:
- `task_conditions`
- `task_condition_types`

Used to capture:

- At height  
- Confined space  
- Hot work  
- Environmental exposure  

👉 Drives **automatic hazard detection**

---

## 7. Risk Assessment Method (Risk Engine)

### Base Risk

Calculated using:

- `severity_levels`
- `probability_levels`
- `risk_matrix`

### Control Adjustment

Using:

- `control_effectiveness_scale`

---

## 8. Bowtie Risk Model (NEW)

Tables:
- `bowtie_threats`
- `bowtie_barriers`
- `bowtie_consequences`

Defines:

- Threats → Causes  
- Barriers → Prevention  
- Consequences → Outcomes  

👉 Aligns with oil & gas risk frameworks.

---

## 9. Barrier Integrity Scoring (NEW)

Barriers are evaluated using:

- Effectiveness  
- Reliability  
- Condition  

Output:

- STRONG  
- MODERATE  
- WEAK  

👉 Weak barriers increase risk score.

---

## 10. Enhanced Risk Engine (UPDATED)

Risk is now calculated using:

- Conditions (task_conditions)
- Control effectiveness
- Barrier penalties

Outputs:

- Base risk score  
- Final risk score  
- Risk classification  

---

## 11. Automation Layer (NEW)

Triggered by events:

- `task_saved`
- `risk_calculated`
- `day_submitted`

Performs:

- Hazard creation  
- Corrective action generation  
- Validation checks  
- Notifications  

---

## 12. How the System Reacts to Problems

### Corrective Action Pathways

1. Observation-driven  
   Observation → Hazard → Action  

2. Incident-driven  
   Task → Hazard → Incident → Intervention → Action  

3. Control failure  
   Hazard → Control → Low effectiveness → Action  

4. Automation-driven (NEW)  
   High risk → Auto action  

---

## 13. Residual Risk & Lifecycle

- Residual severity & probability stored  
- Status tracking:
  - Hazards: Open / Controlled / Closed  
  - Controls: Active / Replaced / Closed  

---

## 14. Simulation Layer (NEW)

Simulates:

- Barrier failure  
- Control degradation  

Outputs:

- Risk change  
- Root cause explanation  
- Recommended actions  

---

## 15. Daily Data Entry

| Table | Purpose |
|------|--------|
| `attendance` | Worker presence |
| `ppe_checks` | PPE compliance |
| `observations` | Unsafe acts/conditions |
| `hazards` | Identified risks |
| `weather` | Environmental factors |

---

## 16. Planning Tables

| Table | Purpose |
|------|--------|
| `ptw` | Work authorization |
| `jsa` | Risk planning |
| `tasks` | Templates |
| `task_execution` | Actual work |

---

## 17. Event-Based Tables

| Table | Purpose |
|------|--------|
| `incidents` | Event occurrence |
| `interventions` | Immediate response |
| `corrective_actions` | Long-term actions |

---

## 18. Daily Submission (NEW)

Table:
- `daily_submission`

Tracks:

- Workflow completion  
- Submission status  

---

## 19. KPI & Analytics Layer (NEW)

Table:
- `analytics.daily_kpis`

Tracks:

- Leading indicators (PPE, controls, conditions)  
- Lagging indicators (incidents, actions)  
- Derived KPIs  

---

## 20. Multi-Site Expansion Rule

Supports:
**Site → Zone → Phase → Task → Task Execution**


---

## 21. Lookup Tables

Used for:

- Standardization  
- Data validation  
- Analytics consistency  

---

## 22. Future Capabilities

- Predictive risk modeling  
- AI-assisted querying  
- Control degradation alerts  
- Cross-site analytics  

---

## 23. Correct Way to Enter Data

### Key Rule:

> “Is this linked to a task?”

### Guidelines:

1. Task-linked → include `task_execution_id`  
2. Not task-linked → use NULL + notes  
3. Always include required fields  

---

## 🧠 In One Sentence

**A structured, audit-ready risk intelligence database that captures, connects, evaluates, and predicts operational safety risk.**
