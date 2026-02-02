# Database Operations Manual
## HSE Risk Intelligence System

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


