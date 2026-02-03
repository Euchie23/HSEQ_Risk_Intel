# 📒 Database Operations Manual 📒
## HSE-Q Risk Intelligence System

---

## 🔐 Data Ethics, Governance & Portfolio Use

This database design is based on field-derived HSE observations, daily safety reports, PPE verification sheets, and operational records authored by the developer during routine site oversight.

The system is **not** built from any proprietary company database, software export, or internal system.

All tasks, hazards, observations, incidents, toolbox topics, and attendance records originate from independent HSE documentation prepared on site and later structured into this relational database for analytics and portfolio demonstration.

### For Portfolio / GitHub Use

To ensure professional data ethics and confidentiality, the following rules are applied when publishing this project:

- Worker names are anonymized in the `PERSON` table
- Site and company identifiers are generalized in the `SITE` and `ZONE` tables
- PTW IDs, JSA IDs, and certification identifiers are anonymized
- Company-specific risk matrices, severity definitions, and probability classifications are abstracted into generic lookup tables
- No proprietary documents, templates, forms, or internal company systems are reproduced

### What This Dataset Represents

The published dataset is a **structured abstraction of real operational patterns** observed on site.

It preserves:

- How tasks create hazards
- How hazards are controlled
- How incidents occur
- How interventions and corrective actions are triggered
- How toolbox meetings, attendance, and PPE checks influence site safety

While ensuring:

> No proprietary company framework, identity, or documentation is exposed.

### Professional Significance

This approach demonstrates how real-world HSE intelligence can be translated into:

- A governed relational database
- Operational dashboards
- Risk analytics
- Future AI-assisted querying

…while strictly adhering to professional data ethics, privacy standards, and confidentiality expectations expected at a consultancy level.

---

## 1. Purpose of the System

This is not an incident log.

This database is a **Risk Intelligence System** designed to:

- Understand risk **before work starts**
- Monitor risk **while work is happening**
- Learn from risk **after events occur**
- Enable predictive analytics in the future

The entire system is **task-centered**. Every record in the database connects back to a task performed on site.

---

## 1. Purpose of the System

This is not an incident log.

This database is a **Risk Intelligence System** designed to:

- Understand risk **before work starts**
- Monitor risk **while work is happening**
- Learn from risk **after events occur**
- Enable predictive analytics in the future

The entire system is **task-centered**. Every record in the database connects back to a task performed on site.

---

## 2. The Golden Rule of the Database

> Nothing happens on site unless it is linked to a **TASK**

This rule ensures the data can be analyzed meaningfully.

The following tables must always reference a `task_id`:

- Attendance
- PPE Checks
- Observations
- Hazards
- Incidents
- Weather

If you cannot link a record to a task, the data is being entered incorrectly.

---

## 3. Work Planning Before Execution

Before any task starts:

1. A **Permit To Work (PTW)** is issued
2. A **Job Safety Analysis (JSA)** is prepared
3. Required **certifications** are verified
4. Only qualified **persons** can execute the task

This ensures risk is controlled **before exposure**.

Tables involved:

- `ptw`
- `jsa`
- `ptw_certifications`
- `jsa_certifications`
- `person_certifications`
- `tasks`

---

## 4. Risk Assessment Method (Risk Engine)

Risk is calculated using three lookup tables:

- `severity_levels`
- `probability_levels`
- `risk_matrix`

These define the **initial risk level** of a hazard.

Risk is then reassessed after controls are applied using:

- `control_effectiveness_scale`

This shows whether controls are **actually reducing risk in practice**.

Tables involved:

- `hazards`
- `hazard_controls`
- `site_controls`

---

## 5. How the System Reacts to Problems

Two pathways can lead to corrective action.

### Path A — From Observations

**Observation → (possible) Incident → Intervention → Corrective Action**

### Path B — From Hazard Reviews


Tables involved:

- `observations`
- `incidents`
- `interventions`
- `corrective_actions`

---

## 6. Daily Data Entry (Operational Monitoring)

These tables are updated **every working day**:

| Table | Purpose |
|---|---|
| `attendance` | Who was present for the task |
| `ppe_checks` | PPE compliance monitoring |
| `observations` | Unsafe acts / unsafe conditions |
| `hazards` | Risk identification during work |
| `weather` | Environmental exposure conditions |

---

## 7. Updated When Work is Planned

| Table | Purpose |
|---|---|
| `ptw` | Work authorization |
| `jsa` | Risk planning |
| `tasks` | Defines work executed |

---

## 8. Updated Occasionally

| Table | Purpose |
|---|---|
| `persons` | Workforce updates |
| `person_certifications` | Renewals / expiries |
| `zones` | Site layout evolution |
| `phases` | Construction progression |
| `site_controls` | Permanent or semi-permanent controls |

---

## 9. Updated Only When Events Occur

| Table | Purpose |
|---|---|
| `incidents` | When something happens |
| `interventions` | Immediate response actions |
| `corrective_actions` | Long-term fixes and tracking |

---

## 10. Multi-Site Expansion Rule

The database is designed to support multiple sites in the future.

Hierarchy:

**Site → Zone → Phase → Task**


This allows the same system to scale across multiple projects while keeping data consistent.

---

## 11. Purpose of Lookup Tables

Lookup tables:

- Standardize reporting
- Prevent data entry errors
- Enable reliable analytics
- Support future machine learning models
- Ensure consistency across sites and time

---

## 12. What This System Enables in the Future

Because every activity links to tasks, this database can support:

- Risk trend analysis
- Unsafe behavior prediction
- Incident likelihood modeling
- PPE non-compliance trends
- Environmental risk correlation

This is the foundation for **predictive safety analytics**.

---

## 13. Correct Way to Enter Data

When entering any record, always ask:

> “Which task was this related to?”

If the answer is unclear, do not enter the data until the task is identified.




