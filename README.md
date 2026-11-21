# SwiftChat System Redesign

<p align="center">
  <img src="docs/images/autofilum-logo.jpeg" alt="AutoFilum logo" width="420">
</p>

A system analysis and design project to redesign **SwiftChat**, a messaging and file-management platform used by medium-sized organisations. It was built as a group project for the **System Analysis and Design (ISYS10242)** module at Nottingham Trent University.

As the fictional IT start-up **AutoFilum** (*"We thread files. You move forward."*), our team analysed the problems with the current SwiftChat platform. We then designed an automated, cloud-based messaging and collaboration system to replace it, covering everything from feasibility and requirements through to UML models, a relational database and UI prototypes.

> This is a **design project**: it holds analysis and design documents, diagrams and a database schema, not a working application.

---

## Table of Contents
- [The Problem](#the-problem)
- [Proposed Solution](#proposed-solution)
- [Methodology](#methodology)
- [Feasibility Study](#feasibility-study)
- [Requirements](#requirements)
- [Use Case Diagram](#use-case-diagram)
- [Class Diagram](#class-diagram)
- [Database Design](#database-design)
- [UI Design](#ui-design)
- [Project Plan](#project-plan)
- [Repository Structure](#repository-structure)
- [Team](#team)

---

## The Problem
As SwiftChat grew, its existing system (a local server with poor data storage) started causing problems:
- **Lost audit logs**, which damaged client trust and accountability
- **Permission management errors**, so users could reach the wrong data
- **Security vulnerabilities**
- **Manual onboarding and admin work**, which wasted staff time

## Proposed Solution
An automated messaging and collaboration management system that:
- **Automates onboarding**: organisations register themselves and get a workspace created after approval
- **Stores data in the cloud** for secure, scalable and reliable storage with real-time access
- **Uses role-based access control** so users only see what they are authorised to see
- **Logs activity in an audit trail** for transparency and accountability
- **Provides analytics and reports** on usage patterns and staff performance
- **Automates billing**, including subscriptions, payments and invoice generation

## Methodology
We chose **Scrum** because the project had a limited budget, a short timeframe (about 5–6 months), unfamiliar technologies and a need for clear schedule visibility.
- Short sprints with reviews and retrospectives give continuous feedback.
- Delivering small increments reduces risk by catching issues early.
- It suits a small team that needs close collaboration.

We also considered **Extreme Programming (XP)**, **Rapid Application Development (RAD)** and **Waterfall**. We rejected them because of weak documentation (XP, RAD) or too little flexibility for changing requirements (Waterfall).

## Feasibility Study
| Area | Summary |
|---|---|
| **Technical** | Replace the local server with a DBMS (PostgreSQL/MySQL), a server-side framework (Node.js/Django), cloud hosting (Azure/AWS), GitHub and SSL/TLS security. |
| **Economic** | £60,000 budget over 5 months, with an estimated return of £80,000. Positive NPV and ROI, and break-even is achievable. |
| **Organisational** | Improves usability, data management, security awareness and organisational structure, with risks identified and mitigated. |

**Budget breakdown**

| Component | Category | Cost |
|---|---|---|
| Team Leader | Project Management | £5,000 |
| Project Manager | Planning & Management | £10,000 |
| System Development | Development | £25,000 |
| Database & Security Manager | Development | £10,000 |
| Client Experience Manager | UI/UX | £6,000 |
| Cloud Infrastructure | Operational | £4,000 |
| **Total** | | **£60,000** |

Each feasibility area includes a risk assessment (for example budget overrun, development delay and low user adoption) with a mitigation for each risk.

## Requirements
We gathered requirements through **interviews** and **questionnaires**. Each requirement was given a priority: **M**andatory, **D**esirable, **O**ptional or **I**mprovement.

**Functional requirements** are grouped by actor:
- **Organisation**: register automatically, get a workspace after approval, configure channels and roles, add/remove employees, manage subscriptions and billing, customise the workspace, view usage reports
- **Employee**: send and receive messages, search chat history, share files, access channels, receive notifications, update profile, mute alerts, react to messages
- **Administrator**: approve organisations, manage permissions, monitor system performance, automate billing and invoices, retrieve logs and reports, send announcements

**Non-functional requirements** cover:
- **Performance**: response within 3 seconds under normal use; scales with users and data
- **Security**: secure login, role-based access, encryption of passwords and billing data, audit trail
- **Availability**: 24/7 apart from maintenance, recovery after failure, browser access
- **Usability**: simple interface, minimal training needed, helpful error messages

## Use Case Diagram
Three actors interact with the system: **Organisation** and **Employee** (primary) and **Administrator** (secondary). The diagram uses associations, `<<include>>` and `<<extend>>`; for example, login is required before most features, and payment processing extends subscription management.

![Use case diagram](docs/images/use-case-diagram.png)

## Class Diagram
The design centres on a **User** superclass, specialised through inheritance into **Organization**, **Employee** and **Administrator**. Supporting classes are **Workspace**, **Channel**, **Subscription**, **Payment**, **ChatHistory**, **Report** and **Notification**, connected by associations with multiplicities (for example, one Organization has many Workspaces). The model applies encapsulation, abstraction, polymorphism and separation of concerns.

![Class diagram](docs/images/class-diagram.png)

## Database Design
The entity relationship diagram was converted into an **11-table relational schema** (MySQL syntax). The full SQL is in [`database/schema.sql`](database/schema.sql).

![Entity relationship diagram](docs/images/erd.png)

| Table | Purpose |
|---|---|
| `Users` | Central table for shared user details (name, email, password, role) |
| `Organization`, `Employee`, `Administrator` | Role-specific tables linked to `Users` |
| `Workspace`, `Channel` | An organisation owns many workspaces; a workspace contains many channels |
| `Subscription`, `Payment` | Plans and billing; a payment must belong to a valid subscription |
| `Notification` | Alerts sent to users |
| `Report`, `Permission` | Administrator reporting and access control |

Primary and foreign keys enforce **referential integrity**, and splitting data into related tables (**normalisation**) reduces redundancy.

## UI Design
Prototype screens for the three portals:

| Organisation Portal | Admin Dashboard | Employee Chat |
|---|---|---|
| ![Organisation portal](docs/images/ui-organisation-portal.jpeg) | ![Admin dashboard](docs/images/ui-admin-dashboard.jpeg) | ![Employee chat](docs/images/ui-employee-chat.jpeg) |
| Approval status, employee management, billing, workspace changes, usage reports | Pending organisations, revenue, active users, activity log, system health | Channel messaging with file and image sharing, reactions and notifications |

## Project Plan
The project was planned with a Gantt chart covering each stage of the work.

![Gantt chart](docs/images/gantt-chart.png)

## Repository Structure
```
├── README.md
├── database/
│   └── schema.sql          # 11-table MySQL schema
└── docs/
    └── images/             # UML diagrams, ERD, UI screens, Gantt chart
```

## Team
| Member | Role | Main contributions |
|---|---|---|
| Excell Moses Efe | Group Leader & UI Designer | UI for the three portals, company logo, introduction |
| **Swagata Paul** | **System Designer** | **Use case diagram, class diagram, feasibility study, functional and non-functional requirements, risk assessments; database design (with two team members); introduction and requirement gathering** |
| Seherin Zaman | Business Analyst | Report structure and editing, methodology, interview questions, requirements ideas, diagram descriptions, database design |
| Hephzibah John Igani | Project Manager & Database Designer | Gantt chart, primary database design |

---
*Module: ISYS10242 System Analysis and Design, Nottingham Trent University.*
