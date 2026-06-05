# Medical Image-Based Disease Detection and Classification System

> **Focus:** This repository implements a complete, professional **Software Engineering Documentation Lifecycle** for a Medical Image-Based Disease Detection and Classification System. The objective is not to train a machine learning model, but to demonstrate rigorous documentation methodology, structured version control, peer review workflows, and formal delivery processes.

---

## 📋 Project Overview

| Item | Details |
| :--- | :--- |
| **Project Title** | Medical Image-Based Disease Detection and Classification System |
| **Focus Area** | Documentation Methodology, Git Version Control, QA Process |
| **Standard Followed** | IEEE Std 830-1998 (SRS), UML 2.x (SDD Diagrams) |
| **Repository** | [GitHub](https://github.com/alirezakavianifar/Medical-Image-Based-Disease-Detection-and-Classification-System.git) |
| **Final Status** | ✅ All 5 phases complete – Release Tag: `v1.0-FINAL` |

---

## 📂 Repository Structure

```text
Medical-Image-Based-Disease-Detection-and-Classification-System/
│
├── docs/                              # All formal documentation artifacts
│   ├── Doc1_Requirements/
│   │   └── SRS.md                     # Software Requirements Specification (IEEE 830)
│   ├── Doc2_Design/
│   │   └── SDD.md                     # Software Design Document (UML + Architecture + API)
│   ├── Doc3_UserGuide/
│   │   ├── Index.md                   # Documentation suite index
│   │   ├── User_Manual.md             # Clinical user guide
│   │   ├── Installation_Guide.md      # Deployment & setup guide
│   │   ├── Test_Report.md             # QA verification test cases and results
│   │   └── API_Documentation.md       # OpenAPI 3.0 REST API specification
│   ├── Final_Report/
│   │   └── Final_Report.md            # Final project report with git log & appendices
│   ├── Project_Charter.md             # Project scope, stakeholders, timeline
│   └── Documentation_Standards.md    # Naming, formatting, and versioning conventions
│
├── diagrams/                          # UML and architecture diagram files (Mermaid)
│   ├── architecture_system_layers.md  # 4-tier system architecture
│   ├── usecase_doctor_interaction.md  # UML Use Case diagram
│   ├── activity_preprocess_workflow.md# UML Activity diagram (clinical workflow)
│   ├── class_detection_engine.md      # UML Class diagram
│   ├── sequence_image_upload.md       # UML Sequence diagram
│   ├── database_schema_erd.md         # Database ERD schema
│   └── gantt_project_timeline.md      # 8-week Project Gantt Chart
│
├── templates/                         # Reusable document templates for future projects
│   ├── SRS_Template.md                # IEEE 830-aligned SRS template
│   ├── SDD_Template.md                # Architecture & design document template
│   ├── Review_Log_Template.md         # Peer review inspection log template
│   └── Final_Report_Template.md       # Final project report template
│
├── reviews/                           # Peer review logs and QA records
│   ├── SRS_Review_Log.md              # SRS peer inspection and approval log
│   ├── SDD_Review_Log.md              # SDD design review and inspection log
│   ├── User_Validation_Report.md      # Doc3 validation role-play report
│   ├── Final_Report_Review_Log.md     # Final report quality audit log
│   ├── Documentation_QA_Plan.md       # QA checklist & Requirements Traceability Matrix
│   └── Pull_Request_Process.md        # Branching conventions and PR workflow guide
│
├── .github/
│   └── pull_request_template.md       # GitHub PR template for all contributions
│
├── plan.md                            # Master step-by-step project plan (28 steps)
├── .gitignore                         # Git ignored files configuration
└── README.md                          # This file
```

---

## 🗂️ Deliverables Summary

| # | Deliverable | File | Status |
| :---: | :--- | :--- | :---: |
| 1 | Software Requirements Specification (SRS) | [SRS.md](docs/Doc1_Requirements/SRS.md) | ✅ Complete |
| 2 | System Design Document (SDD) | [SDD.md](docs/Doc2_Design/SDD.md) | ✅ Complete |
| 3 | Clinical User Manual | [User_Manual.md](docs/Doc3_UserGuide/User_Manual.md) | ✅ Complete |
| 4 | Installation & Deployment Guide | [Installation_Guide.md](docs/Doc3_UserGuide/Installation_Guide.md) | ✅ Complete |
| 5 | QA Test Report | [Test_Report.md](docs/Doc3_UserGuide/Test_Report.md) | ✅ Complete |
| 6 | API Documentation (OpenAPI 3.0) | [API_Documentation.md](docs/Doc3_UserGuide/API_Documentation.md) | ✅ Complete |
| 7 | Final Project Report | [Final_Report.md](docs/Final_Report/Final_Report.md) | ✅ Complete |
| 8 | UML Diagrams (6 types) | [diagrams/](diagrams/) | ✅ Complete |
| 9 | Gantt Chart | [gantt_project_timeline.md](diagrams/gantt_project_timeline.md) | ✅ Complete |
| 10 | Peer Review Logs (3 docs) | [reviews/](reviews/) | ✅ Complete |
| 11 | Documentation QA Plan & RTM | [Documentation_QA_Plan.md](reviews/Documentation_QA_Plan.md) | ✅ Complete |
| 12 | PR Workflow Guide + GitHub Template | [reviews/](reviews/) + [.github/](.github/) | ✅ Complete |

---

## 🪵 Git Branch & Versioning Strategy

This project enforces a structured branching model for quality control:

### Branch Structure

```text
main                    ← Production-ready, approved documents only
  └── develop           ← Integration branch; all phase drafts merge here
        ├── doc1-requirements  ← SRS drafting and peer review
        ├── doc2-design        ← SDD, UML diagrams, architecture
        ├── doc3-userguide     ← User manuals, test reports, API docs
        └── final-report       ← Final project report
```

### Workflow Pipeline

```text
Author writes in phase branch
        ↓
Peer Review Log compiled in reviews/
        ↓
Pull Request opened → doc/* branch → develop
        ↓
Reviewer approves PR → Merged into develop
        ↓
Phase finalized → develop merged into main (--no-ff)
        ↓
Release tag created (v1.0-SRS, v1.0-SDD, v1.0-DOC3, v1.0-FINAL)
```

### Release Tags

| Tag | Description |
| :--- | :--- |
| `v1.0-SRS` | Software Requirements Specification baseline |
| `v1.0-SDD` | System Design Document baseline |
| `v1.0-DOC3` | User, Installation & Test Documentation suite |
| `v1.0-FINAL` | Final delivery archive |

---

## 🚀 How to Navigate This Project

1. **Start with the plan:** Read [plan.md](plan.md) for a complete step-by-step methodology breakdown (28 steps across 6 phases).

2. **Review the Project Charter:** [Project_Charter.md](docs/Project_Charter.md) covers objectives, scope, stakeholders, and the 8-week timeline.

3. **Read Documentation Standards:** [Documentation_Standards.md](docs/Documentation_Standards.md) explains naming conventions, commit rules, and version numbering.

4. **Navigate documents by phase:**
   - **Requirements:** [docs/Doc1_Requirements/](docs/Doc1_Requirements/)
   - **Design:** [docs/Doc2_Design/](docs/Doc2_Design/)
   - **User Guides & Tests:** [docs/Doc3_UserGuide/](docs/Doc3_UserGuide/)
   - **Final Report:** [docs/Final_Report/](docs/Final_Report/)

5. **View UML Diagrams:** All diagrams in [diagrams/](diagrams/) render natively in GitHub (Mermaid.js supported). Open any `.md` file to view the interactive diagram.

6. **Audit the reviews:** [reviews/](reviews/) contains peer inspection checklists, validation reports, and the QA traceability matrix.

---

## 📊 Project Timeline

| Week | Phase | Key Deliverable | Tag |
| :---: | :--- | :--- | :--- |
| 1 | Initialization | Project Charter, Git Setup, Standards | — |
| 2 | Requirements Gathering | Stakeholder interviews, SRS drafting | — |
| 3 | SRS Approval | Approved SRS + Review Log | `v1.0-SRS` |
| 4 | System Architecture | UML Use Case, Activity, Class, Sequence | — |
| 5 | SDD Approval | Approved SDD + Review Log | `v1.0-SDD` |
| 6 | User Documentation | User Manual, Install Guide, Test Report, API Docs | — |
| 7 | QA Reviews | Validation Reports, QA Plan, PR Guides | `v1.0-DOC3` |
| 8 | Final Report & Archive | Final Report + Release | `v1.0-FINAL` |

> See the full [Gantt Chart](diagrams/gantt_project_timeline.md) for detailed task-level timelines.

---

## 📖 Documentation Standards Summary

All documents follow the [Documentation Standards Guide](docs/Documentation_Standards.md):

- **Format:** Markdown (`.md`) with GitHub Flavored Markdown (GFM)
- **Diagrams:** Mermaid.js (renders on GitHub natively)
- **Versioning:** Semantic `vX.Y.Z` (Major.Minor.Patch)
- **Commit Prefix:** `DOC1:`, `DOC2:`, `DOC3:`, `REPORT:`, `INFRA:`
- **Exported artifacts:** `SRS_v1.0.0.pdf`, `SDD_v1.0.0.pdf`, etc.

---

## 🔗 Key Links

- 📋 [Master Plan](plan.md)
- 📄 [SRS (Requirements)](docs/Doc1_Requirements/SRS.md)
- 🏗️ [SDD (Design)](docs/Doc2_Design/SDD.md)
- 📘 [User Manual](docs/Doc3_UserGuide/User_Manual.md)
- 🧪 [Test Report](docs/Doc3_UserGuide/Test_Report.md)
- 📑 [Final Report](docs/Final_Report/Final_Report.md)
- 📊 [Gantt Chart](diagrams/gantt_project_timeline.md)
- 🌐 [GitHub Repository](https://github.com/alirezakavianifar/Medical-Image-Based-Disease-Detection-and-Classification-System.git)
