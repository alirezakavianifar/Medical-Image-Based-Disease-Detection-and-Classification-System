# Final Project Report
## Medical Image-Based Disease Detection and Classification System

---

## 1. Executive Summary

This project establishes a rigorous, professional Software Engineering lifecycle for the **Medical Image-Based Disease Detection and Classification System**. Rather than focusing on coding/training a machine learning model, the target goal was the definition, design, quality verification, and management of the documentation artifacts in a structured version-controlled Git repository.

Over the project course, we successfully created:
1. **Requirements Specifications (SRS):** Built standard functional/non-functional criteria under IEEE 830 recommendations.
2. **System Design Blueprint (SDD):** Mapped system decomposition, 4-tier layer specifications, database tables (ERD), APIs, and UML diagrams.
3. **User, Installation, and Test Guides:** Compiled step-by-step clinical workflows, DevOps server scripts, QA verification reports, and OpenAPI reference manuals.
4. **Quality Assurance Framework:** Integrated peer review logs, QA validation loops reports, standard pull request formats, and semantic version tagging.

The repository history reflects clean branch merges (`doc1-requirements`, `doc2-design`, `doc3-userguide`) and release baseline tags (`v1.0-SRS`, `v1.0-SDD`, `v1.0-DOC3`) mapping out our lifecycle progress.

---

## 2. Catalog of Collected Deliverables

All system artifacts are organized within the repository structure. Below is the catalog of collected files:

### 2.1 Requirements Documentation (Phase 2)
- **Master Specification:** [SRS.md](../Doc1_Requirements/SRS.md) - Functional and non-functional requirements.
- **Review Verification:** [SRS_Review_Log.md](../../reviews/SRS_Review_Log.md) - Peer review inspection and approval log.

### 2.2 System Design Documentation (Phase 3)
- **Master Blueprint:** [SDD.md](../Doc2_Design/SDD.md) - Decoupled component layers, database schema details, UML models (Use Case, Activity, Class, Sequence), and API definitions.
- **Review Verification:** [SDD_Review_Log.md](../../reviews/SDD_Review_Log.md) - Design review log.

### 2.3 User, Deployment, & QA Documentation (Phase 4)
- **Suite Index:** [Index.md](../Doc3_UserGuide/Index.md) - Manuals map and structure.
- **Clinical User Guide:** [User_Manual.md](../Doc3_UserGuide/User_Manual.md) - User dashboards walkthrough and troubleshooting matrix.
- **System Installation Guide:** [Installation_Guide.md](../Doc3_UserGuide/Installation_Guide.md) - CLI setup, dotenv configurations, database bootstrap scripts, and verification tests.
- **QA Test Report:** [Test_Report.md](../Doc3_UserGuide/Test_Report.md) - QA strategy, positive/negative test cases (TC01-TC05), and defect logs.
- **API Spec Reference:** [API_Documentation.md](../Doc3_UserGuide/API_Documentation.md) - OpenAPI 3.0.3 specification (YAML) and cURL request CLI scripts.
- **Review Verification:** [User_Validation_Report.md](../../reviews/User_Validation_Report.md) - Clinical and deployment role-playing verification report.

### 2.4 Quality Assurance Framework (Phase 5)
- **Quality Plan:** [Documentation_QA_Plan.md](../../reviews/Documentation_QA_Plan.md) - Quality checklists, and the Requirements Traceability Matrix (RTM).
- **PR Process Guide:** [Pull_Request_Process.md](../../reviews/Pull_Request_Process.md) - Branching conventions and integration workflows.
- **PR GFM Template:** [pull_request_template.md](../../.github/pull_request_template.md) - GitHub pull request template.

---

## 3. Git Repository Commit History

Below is the graph log of all commits in the repository history, illustrating clean branch integrations and structural commit prefix rules compliance:

```text
* 0c81f1d INFRA: Added Pull Request process guide and GitHub templates
* 4a3ca66 INFRA: Added Documentation Quality Assurance and Review Plan
*   cd24304 INFRA: Merge doc3-userguide into develop
|\  
| * d017b8d DOC3: Added User Validation and Verification log report
| * a2fea0a DOC3: Created OpenAPI REST API specifications reference guide
| * 93a9c50 DOC3: Created QA Test Verification and Report manual
| * 3ba5387 DOC3: Created Installation and Deployment Guide
| * 9e14049 DOC3: Created clinical User Manual guide
| * 1d1aa1c DOC3: Initialized Phase 4 with documentation type index
|/  
*   e229e63 INFRA: Merge doc2-design into develop
|\  
| * 4f2c8bb DOC2: Added SDD peer review and architectural inspection log
| * 2837a68 DOC2: Added Section 7 user interface and API specifications to SDD
| * a07f74c DOC2: Added Section 5 database design and indices schema to SDD
| * 4743edf DOC2: Added Section 4 system architecture to SDD
| * ee2ceb0 DOC2: Added Mermaid UML diagrams to SDD
| * e17a956 DOC2: Initialized SDD document with introduction and component decomposition
|/  
*   a8fd223 INFRA: Merge doc1-requirements into develop
|\  
| * f754d3a DOC1: Added SRS peer review and inspection approval log
| * 6059822 DOC1: Added detailed functional, non-functional, and interface requirements
| * e4d75b7 DOC1: Added Section 2 overall description to SRS
| * 4273668 DOC1: Initialized SRS document with purpose, audience, objectives, scope, and references
|/  
* a58d3ad INFRA: Added documentation and repository standards guide
* 6d9b30b Initialize project structure and configuration
```

---

## 4. Project Activities & Phases Recap

The project lifecycle progressed through five distinct documentation and system engineering phases:

### 4.1 Phase 1: Project Initialization
- **Focus:** Setting scope boundaries and creating version control baselines.
- **Key Activities:**
  - Formulated the Project Charter defining clinical objectives, scope boundaries, and milestones.
  - Initialized Git environments with a staging directory structure (`docs/`, `diagrams/`, `templates/`, `reviews/`).
  - Drafted repository [.gitignore](../../.gitignore) and [README.md](../../README.md) guides.
  - Established naming conventions, version rules, and commit message tags in [Documentation_Standards.md](../Documentation_Standards.md).

### 4.2 Phase 2: Requirements Analysis (SRS)
- **Focus:** Specifying functional and non-functional requirements.
- **Key Activities:**
  - Authored standard [SRS.md](../Doc1_Requirements/SRS.md) mapping target clinical audiences, in-scope components, and glossary terms.
  - Documented five functional requirements (FR-01 to FR-05) specifying input, processing, and output steps for user logins, image uploads, AI classification, dashboard canvas drawings, and PDF reports.
  - Logged peer inspection findings (addressing VRAM limitations and user role permissions) and signed off approvals in [SRS_Review_Log.md](../../reviews/SRS_Review_Log.md).
  - Merged requirements to the release branch and tagged the baseline `v1.0-SRS`.

### 4.3 Phase 3: System Design Document (SDD)
- **Focus:** Detailing architectures, data structures, and interface models.
- **Key Activities:**
  - Authored system design blueprint [SDD.md](../Doc2_Design/SDD.md).
  - Created Mermaid.js UML diagrams: Use Case (permissions boundary), Activity (data lifecycle flow), Class (attributes/methods schemas), and Sequence (runtime communication sequence).
  - Designed a 4-tier layered architecture (Presentation UI, Web API Logic, AI Inference, SQLite database).
  - Specified database ERD schemas, data dictionaries, indices, and constraints.
  - Documented REST API route endpoints and UI pane hierarchies.
  - Logged design validations (VRAM process thread locks and database performance search indices) in [SDD_Review_Log.md](../../reviews/SDD_Review_Log.md) and tagged baseline `v1.0-SDD`.

### 4.4 Phase 4: User, Installation, & Test Guides
- **Focus:** Creating manuals, setup guides, and verification logs.
- **Key Activities:**
  - Created [Index.md](../Doc3_UserGuide/Index.md) mapping guides to target audiences.
  - Authored clinical [User_Manual.md](../Doc3_UserGuide/User_Manual.md) with dashboard navigation and troubleshooting steps.
  - Drafted DevOps [Installation_Guide.md](../Doc3_UserGuide/Installation_Guide.md) covering environment configurations and database bootstrap scripts.
  - Compiled [Test_Report.md](../Doc3_UserGuide/Test_Report.md) logging test cases (TC01-TC05) with a 100% success rate.
  - Generated [API_Documentation.md](../Doc3_UserGuide/API_Documentation.md) outlining OpenAPI 3.0.3 YAML contracts and cURL request CLI commands.
  - Logged validation role-play walkthroughs in [User_Validation_Report.md](../../reviews/User_Validation_Report.md) and tagged baseline `v1.0-DOC3`.

### 4.5 Phase 5: Documentation Quality Assurance
- **Focus:** Constructing auditing tools and integration workflows.
- **Key Activities:**
  - Compiled [Documentation_QA_Plan.md](../../reviews/Documentation_QA_Plan.md) establishing checklists (Completeness, Consistency, Traceability, Formatting, Grammar) and the Requirements Traceability Matrix (RTM).
  - Formulated [Pull_Request_Process.md](../../reviews/Pull_Request_Process.md) establishing branch naming rules (`doc/*`, `review/*`, `infra/*`).
  - Implemented standard GitHub template [.github/pull_request_template.md](../../.github/pull_request_template.md).

---

## 5. Version Control & Release Management

To maintain repository clean state, a strict branching and integration pipeline was enforced:

- **Branch Isolation:** No direct commits to `main` or `develop`. Features were authored on phase branches (e.g. `doc1-requirements`, `doc2-design`).
- **Integration Gateway:** Feature branches merged into `develop` integration branch only after peer review logs were compiled.
- **Release Baselines:** When a project phase was finalized, `develop` was merged into `main` using non-fast-forward (`--no-ff`) commits to record the merge, and tagged with semantic release tags (`v1.0-SRS`, `v1.0-SDD`, `v1.0-DOC3`).

---

## 6. Challenges & Lessons Learned

During the design and quality assurance cycles, several challenges were addressed:

1. **Clinical Data Privacy Compliance:** Designing relational database tables that satisfy HIPAA data privacy regulations while ensuring quick dashboard lookup speeds. Resolving this required strict user role checks and separating local binary caches from DB metadata tables.
2. **Synchronizing Code Logic with Documentation:** Syncing code fixes (such as limiting uvicorn threads to 1 to prevent GPU memory crashes, and adding SQLite query indices) with the SDD architecture tables and Installation manuals.
3. **Review Process Coordination:** Managing the technical documentation review logs across multiple stakeholder roles (Lead Architect, QA Lead, Hospital Clinical Advisory, Project Supervisor) to keep the project timeline on schedule.

---

## 7. Project Delivery Status

### 7.1 Deliverables Status Checklist

- [x] Project Charter & Repository Setup (`docs/Project_Charter.md`) -> **Complete**
- [x] Naming & Commit standards (`docs/Documentation_Standards.md`) -> **Complete**
- [x] Software Requirements Specification (`docs/Doc1_Requirements/SRS.md`) -> **Complete**
- [x] Requirements Peer Review Log (`reviews/SRS_Review_Log.md`) -> **Complete**
- [x] System Design Document (`docs/Doc2_Design/SDD.md`) -> **Complete**
- [x] System Design Peer Review Log (`reviews/SDD_Review_Log.md`) -> **Complete**
- [x] Clinical User Manual (`docs/Doc3_UserGuide/User_Manual.md`) -> **Complete**
- [x] Deployment & Installation Guide (`docs/Doc3_UserGuide/Installation_Guide.md`) -> **Complete**
- [x] QA Verification Test Report (`docs/Doc3_UserGuide/Test_Report.md`) -> **Complete**
- [x] OpenAPI API reference specification (`docs/Doc3_UserGuide/API_Documentation.md`) -> **Complete**
- [x] Clinical & Deployment Validation Report (`reviews/User_Validation_Report.md`) -> **Complete**
- [x] Documentation QA Plan & Traceability Matrix (`reviews/Documentation_QA_Plan.md`) -> **Complete**
- [x] Pull Request workflows guide (`reviews/Pull_Request_Process.md`) -> **Complete**
- [x] GitHub Pull Request GFM Template (`.github/pull_request_template.md`) -> **Complete**
- [/] Final Project Report (`docs/Final_Report/Final_Report.md`) -> **In Progress** (Awaiting Final Release)

### 7.2 Future Improvements
- **Integration of HL7 / FHIR Standards:** Future backend iterations should incorporate standard healthcare communication protocols to link directly to clinical PACS databases.
- **CI/CD Pipeline Automation:** Integrating GitHub Actions to run automated OpenAPI schema compliance checks and run Markdown linter validations on every PR commit.

---

## 8. Appendices

### Appendix A: Weekly Timeline Matrix

| Week | Phase | Major Deliverable | Status |
| :--- | :--- | :--- | :---: |
| **Week 1** | Project setup and Git repository initialization | Project Charter, readme, standards guidelines | **PASSED** |
| **Week 2** | Requirements gathering | Elicitation notes, literature review | **PASSED** |
| **Week 3** | SRS creation and approval | Baseline SRS document, review checklist logs (`v1.0-SRS`) | **PASSED** |
| **Week 4** | System design and UML diagrams | UML Use case, Activity, Class, Sequence diagrams | **PASSED** |
| **Week 5** | SDD review and approval | Baseline SDD document, review checklist logs (`v1.0-SDD`) | **PASSED** |
| **Week 6** | User, installation, and test documentation | Clinical manual, install guide, test cases, OpenAPI specs | **PASSED** |
| **Week 7** | Documentation reviews and revisions | Validation role-play reports, QA plan, PR templates (`v1.0-DOC3`) | **PASSED** |
| **Week 8** | Final report, release tagging, project archive | Final report, release tag merge to main (`v1.0-FINAL`) | **IN PROGRESS** |

### Appendix B: Architectural UML Models
System diagrams (Use Case, Activity, Class, Sequence) are rendered in [SDD Section 3](../Doc2_Design/SDD.md#3-design-models--uml-diagrams).

### Appendix C: Peer Review & Inspection Logs
Review logs and audit trails are documented in:
- [SRS Review Log](../../reviews/SRS_Review_Log.md)
- [SDD Review Log](../../reviews/SDD_Review_Log.md)
- [User/Deployment Validation Report](../../reviews/User_Validation_Report.md)
