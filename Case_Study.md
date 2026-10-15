# 🦺 HSE Risk Intelligence  

## Operational HSE Decision Support System

---

## 🧭 Decision Context

Operational HSE work can generate information across many separate records:

- daily reports
- workforce attendance
- toolbox meetings
- PTWs and JSAs
- task records
- observations
- hazards and controls
- incidents
- corrective actions
- emergency-preparedness activities

The challenge is not simply collecting more information.

The challenge is preserving enough context and relationships to understand what happened, what required attention, what action followed, and what management ultimately reviewed.

HSE Risk Intelligence was developed as a personal project exploring how operational HSE information can be represented as a connected, traceable decision-support system rather than a collection of disconnected forms and spreadsheets.

---

## 🎯 Problem Framing

A useful operational system should help answer questions such as:

- What work was actually performed?
- Who was present?
- Where did the work occur?
- What conditions were present?
- What was observed?
- What hazards were identified?
- Which controls were associated with those hazards?
- Did an incident occur?
- What immediate controls or follow-up were required?
- Which corrective actions remain outstanding?
- Were completed actions verified?
- What preparedness activities occurred?
- What information was ultimately confirmed for management?

The project therefore focuses on traceability and operational context before advanced analytics.

---

## 👥 Intended Users

The architecture is designed around potential use by:

- HSE personnel
- site supervisors
- project managers
- consultants
- operational management
- auditors or reviewers

Version 1 remains human-guided: the system structures and surfaces evidence, while professional judgement remains with the user.

---

## 🧱 Version 1 Scope

The current system includes:

Operational Foundation

- sites
- sections
- zones
- phases
- personnel
- organizations
- teams
- application-user/site access

Planning

- Planned Work Packages
- planned tasks
- PTWs
- JSAs
- Method Statements
  
Daily Operations

- work date and field sessions
- attendance
- toolbox activity
- task execution
- PPE/control verification
- weather-assisted context

Risk & Assurance

- observations
- hazards
- hazard controls
- severity/probability classification
- control status and effectiveness
- corrective actions
- verification and closure

Incident / Event Management

- incident/event capture
- people and assets involved
- incident controls
- observation/task relationships
- status history
- follow-up and investigation context
- external file references

Emergency Preparedness

- drill lifecycle
- participants
- lessons learned
- improvement areas
- links to operational records and corrective actions

Confirmation & Reporting

- controlled daily confirmation
- locked confirmation batches
- immutable management-report snapshots
- Word report generation

---

## 🔄 Operational Data Model

At a high level, the platform follows this pattern:

Operational Foundation
→ Planning & Field Work
→ Risk Detection
→ Incident Response
→ Corrective Follow-Up & Assurance
→ Confirmed Management Reporting

The underlying PostgreSQL database contains additional relationship, lookup, lifecycle, audit, approval, and history tables that support this conceptual model.

---

## 🏗️ Planned Work vs Actual Work

One important design decision was separating planned scope from actual execution.

A Planned Work Package can describe reusable or longer-running intended work.

A task_execution represents a specific dated instance of work actually performed.

This prevents the system from treating:

> “This activity was planned”

as equivalent to:

 > “This activity actually occurred today.”

PTW, JSA, Method Statement, personnel, weather, hazards, and other operational records can then be interpreted against the appropriate planning or execution context.

---

## 👁️ Observations, Hazards & Controls

Observations do not need to be attached artificially to a task to remain valid.

Where evidence supports the relationship, an observation can connect to:

**Task Execution → Observation → Hazard → Hazard Control**

Hazards may also arise through other operational paths.

Controls preserve information about implementation status and effectiveness rather than assuming that the existence of a control means the risk has been adequately managed.

This distinction allows the database to preserve both:

- control presence
- control assurance

---

## 🚨 Incident Architecture

Incidents are treated as standalone events at capture.

The system deliberately avoids forcing every event through:

**Incident → Hazard → Control**

before the incident can be recorded.

After capture, an incident may be related to:

- task executions
- observations
- people
- assets
- weather
- incident-specific controls
- external notifications
- supporting file references
- lifecycle/status history

This keeps initial event capture practical while allowing richer relationships to be established later.

---

## ✅ Corrective Action Lifecycle

Corrective actions provide longer-term follow-up.

Actions may originate from sources including:

- observations
- hazards
- hazard controls
- incidents
- planning documentation
- inspections/audits
- management concerns

The architecture separates:

**Completion**

from:

**Verified Closure**

This prevents an action from being treated as fully resolved simply because somebody marked the work complete.

---

## 🚒 Emergency Preparedness

Emergency Drills are represented as operational records with their own lifecycle.

They can capture:

- drill type
- participants
- objectives
- sequence of events
- positive findings
- improvement areas
- lessons learned
- recommendations
- follow-up

Drills can also be linked to tasks, incidents, observations, hazards, and corrective actions.

This enables preparedness activity to contribute to broader operational learning rather than existing as an isolated compliance record.

---

## 🔒 Daily Confirmation & Immutable Reporting

A major Version 1 design decision was separating an unfinished operational day from a formally confirmed record.

At final confirmation:

  1. the relevant site/date/section batch is confirmed and locked;

  2. the final management report is preserved as a snapshot;

  3. the canonical confirmed report can later be retrieved without reconstructing it from changing operational tables.

This improves historical traceability.

The Word version may be downloaded and edited externally, while the system-preserved snapshot remains unchanged.

---

## 🧪 Technical Approach

Application

- Python
- Streamlit

Database

- PostgreSQL
- relational schemas separated into lookup, core, operations, security, and analytics
- explicit primary/foreign-key relationships
- controlled lookup dictionaries
- lifecycle/history tables
- approval structures
- reusable canonical database baseline

Reporting

- structured management-report generation
- Word export
- immutable confirmed-report snapshots

Deployment Architecture

- local PostgreSQL during development
- portable canonical SQL baseline
- cloud PostgreSQL deployment planned on Neon

---

## 🗄️ Reproducible Database Baseline

During Version 1 stabilization, years of incremental SQL changes were consolidated into a canonical PostgreSQL baseline.

The canonical build was tested against an empty PostgreSQL database.

This established a reproducible starting point containing:

- current schemas
- final table structures
- lookup/reference data
- core baseline data
- security baseline data
- reusable task templates
- constraints and indexes

Historical operational test records were intentionally excluded.

Future database changes are intended to be applied as forward migrations rather than continuously rewriting the frozen Version 1 baseline.

---

## 📊 Analytics Philosophy

Version 1 prioritizes trustworthy operational capture before predictive analytics.

Because records are structured relationally, future analysis can examine:

- recurring hazards
- incident patterns
- observation trends
- corrective-action ageing
- control effectiveness
- preparedness activity
- zone/task exposure
- organizational or team patterns
- longitudinal and cross-site trends

The project does not currently represent those possibilities as a mature predictive-risk engine.

---

## ⚠️ Limitations

Version 1 is still a developing personal project.

Important limitations include:

- deployment optimization is still in progress
- cloud deployment is not yet the production source of truth
- advanced management dashboards remain future work
- analytics depend on the quality and completeness of operational data
- the platform supports, but does not replace, professional HSE judgement
- bow-tie modeling, barrier-health analysis, simulations, and AI-assisted querying are not current Version 1 capabilities

---

## 💡 Key Lessons

Several design lessons emerged during development:

- A clear operational data model can be more valuable than prematurely adding sophisticated analytics.
- Planned work and actual work should not be treated as the same thing.
- Operational relationships should be captured when evidence supports them, not because the schema allows them.
- Incident capture must remain practical even when full causal context is not yet known.
- A control should not automatically be assumed effective.
- Corrective-action completion and verification are different lifecycle events.
- Historical confirmed reports should not silently change when later records change.
- Complex architecture should be justified by an operational need rather than hypothetical future requirements.

----

## 🔭 Version 2 Research Direction

Once Version 1 is deployed and generating stable operational data, future development may explore:

- bow-tie hazard visualization
- barrier/control-health analysis
- control degradation indicators
- what-if scenario simulation
- emergency-preparedness simulation
- evidence-linked photographs stored outside PostgreSQL
- richer management dashboards
- cross-site and longitudinal analytics
- natural-language querying
- assisted pattern detection

The purpose of Version 2 would be to investigate what additional intelligence can responsibly be derived from the operational evidence already captured by Version 1.

---

## 🎯 Executive Takeaway

HSE Risk Intelligence demonstrates how operational HSE information can move from fragmented records toward a connected, auditable decision-support architecture.

The value of Version 1 is not that the application makes safety decisions automatically.

Its value is that it preserves the relationships necessary for people to make better-informed decisions:

**Work → Evidence → Risk → Controls → Follow-Up → Verification → Management Record**

🧠 In One Sentence

HSE Risk Intelligence transforms fragmented operational HSE records into a connected, traceable PostgreSQL-backed workflow for human-guided risk management and management reporting.
