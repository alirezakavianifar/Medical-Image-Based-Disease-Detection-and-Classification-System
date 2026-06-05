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
