# 📒 Database Operations Manual 📒
## HHSE Risk Intelligence — Version 1

---

## 🔐 Data Ethics, Governance & Portfolio Use

This database design is informed by field-derived HSE observations, daily reporting, PPE/control verification, planning documentation, emergency-preparedness activities, and operational records.

The system is not built by reproducing a proprietary company database or internal HSE software system.

### For Portfolio / GitHub Use

- personnel identities are anonymized or generalized
- site and company identifiers are abstracted where appropriate
- PTW, JSA, and related reference numbers are generalized
- proprietary forms and internal templates are not reproduced
- lookup structures and workflow logic are implemented independently

The model preserves realistic operational relationships while protecting confidential information.

---

## 1. Purpose of the System

HSE Risk Intelligence is not simply an incident register.

Version 1 is a human-guided operational HSE decision-support system designed to connect:

**Planning → Field Work → Observations → Hazards → Controls → Incidents → Corrective Actions → Verification → Confirmed Reporting** 

The database provides traceability across those relationships while preserving site, section, zone, personnel, organization, work-date, and application-user context.

The architecture is informed by common HSE-management practices and ISO 45001-style concepts such as hazard identification, operational control, incident follow-up, corrective action, worker participation, documented information, and continual improvement.

It should not be interpreted as certification against ISO 45001 or as a replacement for professional HSE judgement.

---

## 2. Operational Foundation

Core context includes:

- sites
- site sections
- zones
- zone models
- zone lineage
- phases
- organizations
- teams
- personnel
- personnel / organization history
- consultant section assignments

Operational records should retain enough context to answer:

- Where did this occur?
- When did it occur?
- Which work activity was involved?
- Who was present?
- Which organization or team was involved?
- Which section or zone governed the activity?
  
---

## 3. Planning Before Execution

Formal planning records include:

- planned_work_package
- planned_work_task
- ptw
- jsa
- method_statements

A Planned Work Package represents reusable planned scope.

A task_execution represents an actual dated instance of work.

These concepts must remain separate:

> Planned Work = intended scope 

> Task Execution = what actually happened

PTW, JSA, and Method Statement records may be associated with planned work and/or execution according to the current workflow and database relationships.

---

## 4. Toolbox & Workforce Participation

Toolbox meetings provide the operational bridge between documented planning and actual field conditions.

The platform can capture:

- toolbox occurrence
- topics discussed
- personnel participation
- planned-work relationships
- hazard discussion
- operational context

Toolbox meetings are not substitutes for PTW or JSA documentation.

They capture discussion and preparedness at the field-operational level.

---

## 5. Attendance & Personnel

Personnel presence is captured through attendance structures associated with the operational date and shift/session.

Personnel belong to organizational structures and may participate in teams.

Historical organizational relationships should be preserved rather than overwritten where practical.

Personnel status changes may be subject to controlled approval workflows.

---

## 6. Task Execution

task_execution represents actual field work.

Task executions may connect to:

- reusable task templates
- planned work
- teams / personnel context
- shift/session
- weather
- observations
- hazards
- incidents
- PPE/control verification
- planning documentation

A task execution must describe actual work rather than act as a generic planning record.

---

## 7. Weather & Operational Conditions

Weather data provides operational context.

The current platform supports assisted weather capture and stores environmental variables with source traceability.

Weather may be linked to task execution and incidents where relevant.

Condition-threshold and hazard-library structures provide a foundation for future assisted risk interpretation, but Version 1 should remain human-guided rather than presenting automated risk scoring as a final safety decision.

---

## 8. Observations

Observations represent field findings that may or may not be associated with a task execution.

An observation may:

- identify an unsafe or noteworthy condition
- be linked to operational work
- produce or relate to hazards
- become associated with an incident
- lead to corrective action

Observations should remain valid even when they are not task-linked.

The key principle is:

> Operational traceability should be captured when known without forcing artificial relationships when the evidence does not support them.

---

## 9. Hazards

Hazards may arise from:

- task execution
- observations
- planned-work context
- newly identified execution conditions
- hazard-library references

Hazard records may include:

- hazard classification
- description
- severity
- probability
- operational source
- status
- associated observation
- task / planned-work provenance
- controls

Version 1 stores structured risk information but does not claim to perform a fully automated predictive-risk calculation engine.

---

## 10. Hazard Controls

hazard_controls connects identified hazards with controls.

Controls may include:

- implementation status
- effectiveness assessment
- notes
- shift context
- replacement relationships

Control effectiveness uses a structured scale, allowing records to distinguish states such as pending review, ineffective, weak, adequate, strong, or highly effective.

Control information supports human review and corrective-action decisions.

---

## 11. Incident / Event Records

Incidents are standalone operational records.

The system does not require every incident to be forced through:

**Incident → Hazard → Control**

at initial capture.

Incident records may later be related to:

- task execution
- observations
- people
- assets
- external notifications
- controls
- weather
- attachments / external file references
- lifecycle history

Incident linkage may occur directly or through controlled link requests.

The aim is to capture the event first and add relationships when evidence supports them.

---

## 12. Incident Controls & Follow-Up

Incident controls record immediate or event-specific measures associated with an incident.

They may capture:

- control description
- timing
- implementation details
- responsible internal or external person
- effectiveness
- status
- notes

These controls are distinct from persistent hazard controls.

---

## 13. Corrective Actions

Corrective actions represent longer-term follow-up and accountability.

Supported source categories include:

- Incident
- Hazard
- Observation
- Audit
- Inspection
- PTW
- JSA
- Environmental
- Quality
- Management
- Hazard Control

Corrective actions may include:

- action description
- priority
- responsible person
- due date
- lifecycle status
- implementation
- verification
- closure
- notes

Typical lifecycle states include:

- Open
- In Progress
- On Hold
- Completed
- Implemented — Pending Verification
- Verified Closed
- Cancelled
- Overdue

Verification is intentionally distinct from merely marking work as completed.

---

## 14. Emergency Preparedness

Emergency Drills are site/date/section operational records rather than task-only records.

The drill architecture supports:

- drill type
- Details Pending / Completed / Void lifecycle
- participants
- coordinator
- sequence of events
- objectives
- observations
- positive findings
- areas for improvement
- lessons learned
- recommendations
- follow-up drill relationships
  
Drills may be linked to:

- task executions
- incidents
- observations
- hazards
- corrective actions

This allows preparedness activities to contribute to the broader operational-learning record.

---

## 15. Daily Operations Confirmation

Daily Operations can be finalized through a controlled confirmation process.

daily_confirmation_batches records confirmation for the relevant:

- site
- work date
- section

The confirmed batch acts as a lock boundary for the daily operational record.

Records should not be silently reconstructed or altered after final confirmation.

---

## 16. Confirmed Management Report Snapshot

The system preserves the final management report in:

daily_management_report_snapshots

The snapshot is tied to a confirmation batch.

Its purpose is to preserve the report as it existed when the daily record was confirmed.

This prevents a later database change from silently changing the historical confirmed report.

Downloaded Word documents remain editable outside the system, but the canonical stored report remains unchanged.

---

## 17. Guided Workflow Drafts

Guided Streamlit workflows may persist draft state.

Draft records support continuity but must remain distinguishable from confirmed operational records.

Confirmation and management reporting must not accidentally treat unfinished draft state as final operational evidence.

---

## 18. Data Quality & Approval Controls

The architecture includes supporting structures for:

- application-user identity
- site access
- approval requests
- lifecycle history
- data-quality review
- management-controlled transitions

These structures support governance without forcing all decisions into automated rules.

---

## 19. Analytics

The analytics schema provides a foundation for KPI and longitudinal analysis.

analytics.daily_kpis exists as an analytics structure, but Version 1 documentation should not imply that a mature predictive analytics suite is already operational.

Current priority is reliable operational capture and traceability.

Future analytics can derive:

- hazard trends
- observation patterns
- incident patterns
- corrective-action ageing
- control effectiveness
- preparedness activity
- organization / team trends
- work-type exposure
- cross-site or longitudinal comparisons

---

## 20. Multi-Site & Zone Evolution

The architecture supports multiple sites.

Site structure includes:

**Site → Section → Zone**

Zone models and zone lineage allow future physical-site changes to preserve historical interpretation when zones:

- expand
- shrink
- split
- merge
- are replaced

Historical operational records should remain interpretable against the zone structure that existed at the time.

---

## 21. Lookup Tables

Lookup tables provide controlled values for:

- statuses
- categories
- severity
- probability
- control effectiveness
- source types
- drill types
- incident types/subtypes
- shifts
- PPE
- work and lifecycle classifications

Lookups support standardization and reporting consistency.

---

## 22. Version 2 Research Direction

Version 2 may explore how accumulated Version 1 data can support:

- bow-tie visualization
- barrier / control-health analysis
- control-degradation indicators
- scenario simulation
- preparedness simulations
- richer KPI dashboards
- evidence-linked photographs and files stored outside PostgreSQL
- cross-site analytics
- natural-language querying
- assisted pattern detection

These are future capabilities and must not be represented as existing Version 1 functionality until implemented and tested.

---

## 23. Data Entry Principle

A useful question remains:

> “What operational evidence is this record actually connected to?”

Relationships should be created when they improve traceability and are supported by evidence.

Do not create relationships solely because the database technically allows them.

---

## 🧠 In One Sentence

HSE Risk Intelligence is a structured, audit-ready operational data system that connects field work, observations, hazards, controls, incidents, corrective actions, preparedness, and confirmed management reporting to support human HSE decision-making.
