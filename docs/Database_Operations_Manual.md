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
- How observations identify task-unrelated hazards
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

The system is **task-centered where applicable**, but **observations can exist independently** of tasks to capture site hazards or unsafe acts.

---

## 2. Observations Update Rule

| Column | Notes |
|--------|-------|
| `observation_id` | PK |
| `observation_date` | Date of observation |
| `person_id` | Reporter |
| `task_id` | Nullable; may not be linked to a task |
| `phase_id` | Phase observed (optional if task not linked) |
| `observation_type_id` | Type of observation |
| `description` | Observation description |
| `validated_by` | Reviewer |
| `linked_incident_id` | FK incidents (nullable) |
| `validation_outcome` | Observation outcome |
| `notes` | Optional context (e.g., location within site, PPE check reference) |

> Observations **not linked to a task** are still actionable and may identify hazards and trigger incidents, interventions, and corrective actions.

---

## 3. Task-Linked Records

When tasks exist, they drive most operational records:

- Attendance
- PPE Checks
- Hazards
- Incidents
- Weather
- Task-specific observations

Records must reference a `task_id` **if applicable**.

---

## 4. Work Planning Before Execution

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

## 5. Risk Assessment Method (Risk Engine)

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

## 6. How the System Reacts to Problems

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

## 7. Daily Data Entry (Operational Monitoring)

These tables are updated **every working day**:

| Table | Purpose |
|---|---|
| `attendance` | Who was present for the task |
| `ppe_checks` | PPE compliance monitoring |
| `observations` | Unsafe acts / unsafe conditions |
| `hazards` | Risk identification during work |
| `weather` | Environmental exposure conditions |

---

## 8. Updated When Work is Planned

| Table | Purpose |
|---|---|
| `ptw` | Work authorization |
| `jsa` | Risk planning |
| `tasks` | Defines work executed |

---

## 9. Updated Occasionally

| Table | Purpose |
|---|---|
| `persons` | Workforce updates |
| `person_certifications` | Renewals / expiries |
| `zones` | Site layout evolution |
| `phases` | Construction progression |
| `site_controls` | Permanent or semi-permanent controls |

---

## 10. Updated Only When Events Occur

| Table | Purpose |
|---|---|
| `incidents` | When something happens |
| `interventions` | Immediate response actions |
| `corrective_actions` | Long-term fixes and tracking |

---

## 11. Multi-Site Expansion Rule

The database is designed to support multiple sites in the future.

Hierarchy:

**Site → Zone → Phase → Task**


This allows the same system to scale across multiple projects while keeping data consistent.

---

## 12. Purpose of Lookup Tables

Lookup tables:

- Standardize reporting
- Prevent data entry errors
- Enable reliable analytics
- Support future machine learning models
- Ensure consistency across sites and time

---

## 13. What This System Enables in the Future

Because most activities link to tasks—but some observations can exist independently—the database can support:

- **Task-linked analytics:**  
  - Risk trend analysis per task, phase, or zone  
  - Unsafe behavior prediction during specific tasks  
  - Incident likelihood modeling tied to task execution  
  - PPE non-compliance trends for planned work  
  - Environmental risk correlation by task location and phase

- **Task-independent analytics:**  
  - General site hazard tracking (e.g., perimeter issues, unsafe conditions)  
  - Observations that trigger interventions or corrective actions without being tied to a specific task  
  - Longitudinal monitoring of safety trends across zones and phases  

This dual capability lays the foundation for **predictive safety analytics** that reflect real-world operational complexity.

---

## 14. Correct Way to Enter Data

When entering any record, always ask:

> “Is this observation or event linked to a specific task?”

**Guidelines:**

1. **Task-linked records:**  
   - Attendance, PPE checks, hazards, incidents, and most observations should reference a `task_id`.  
   - This ensures accurate risk scoring and trend analysis at the task level.

2. **Task-independent observations:**  
   - Use this when a hazard, unsafe condition, or general observation **cannot be tied to a specific task**.  
   - Enter `task_id` as **NULL** and provide context in the `notes` field (e.g., location, zone, or phase).  
   - These records can still trigger incidents, interventions, and corrective actions.

3. **Mandatory fields:**  
   - Always include `observation_date`, `person_id`, `observation_type_id`, and a clear `description`.  
   - Use `notes` for any additional context.

> Entering records correctly ensures both **task-level precision** and **general site safety intelligence** are preserved.



