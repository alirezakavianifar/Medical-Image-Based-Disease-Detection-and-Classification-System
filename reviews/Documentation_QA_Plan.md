# Documentation Quality Assurance & Review Plan

This document establishes the Quality Assurance (QA) standards, checklists, traceability mechanisms, and review lifecycles used to audit all deliverables in this repository.

---

## 1. Documentation Review Checklists

Every document (SRS, SDD, User Guide, Installation Guide, Test Report, Final Report) must pass inspection against these five core criteria before merging:

### 1.1 Completeness Checklist
- Are all standard template sections present (e.g. IEEE 830 sections for the SRS, 4-tier layers for the SDD)?
- Are system boundaries clearly defined (In-Scope vs. Out-of-Scope)?
- Are all functional requirements (FR) and non-functional requirements (NFR) accounted for?
- Do manuals contain required troubleshooting logs, CLI parameters, and verification health checks?

### 1.2 Consistency Checklist
- Is terminology and glossary acronyms consistent across all files (e.g. DICOM, PACS, CNN, VRAM)?
- Do database fields listed in the SDD match the schema migration scripts exactly?
- Do REST API pathways, payloads, and response status codes match between SDD Section 7 and the OpenAPI specs?

### 1.3 Traceability Checklist
- Can every functional requirement (FR-01 to FR-05) be traced directly to a design component, a database table, a REST route, and a test case?
- Are out-of-scope exclusions traced to design boundaries (e.g. PACS integration treated as out-of-scope, thus excluded from class diagrams and APIs)?

### 1.4 Formatting Checklist
- Does each document have exactly one H1 header?
- Do sub-headers follow a logical nested order (`## H2` -> `### H3` -> `#### H4`)?
- Are lists, tables, and alerts (GitHub admonitions) formatted correctly?
- Do Mermaid.js diagram blocks render without syntax warnings?

### 1.5 Grammar Checklist
- Is all technical text written in professional, academic, clear English?
- Are spelling, syntax, and punctuation correct?
- Is active or passive voice used consistently?

---

## 2. Requirements Traceability Matrix (RTM)

This matrix establishes bidirectional traceability linking requirements to design, persistence schemas, endpoints, and testing verification cases:

| Req ID | Requirement Title | SRS Section | SDD Component | DB Table Target | API Route Endpoint | Test Case ID |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **FR-01** | User Authentication | Section 3.1 | Auth Module (Sec 2.2 / 4.2) | `users` | `POST /api/auth/login` | **TC01** / **TC04** |
| **FR-02** | DICOM Image Upload | Section 3.2 | Image Manager (Sec 2.3 / 4.3) | `images` | `POST /api/images/upload` | **TC02** / **TC05** |
| **FR-03** | AI Image Inference | Section 3.3 | AI Inference (Sec 2.4 / 4.4) | `results` | `GET /api/predictions/{id}` | **TC03** |
| **FR-04** | Dashboard Renders | Section 3.4 | UI Client (Sec 2.1 / 4.2) | `images`, `results` | `GET /api/predictions/{id}` | **TC03** |
| **FR-05** | PDF Report Export | Section 3.5 | Report Compiler (Sec 2.5 / 4.3) | `reports` | `POST /api/reports/export` | **TC04** |

---

## 3. Document Review Lifecycle Workflow

Every documentation phase must strictly follow this review and integration workflow pipeline:

```text
+-----------------------+
|  1. Authoring Draft   |  - Author checkouts feature branch.
|                       |  - Writes/edits Markdown source documents.
+-----------+-----------+
            |
            v
+-----------------------+
|   2. Peer Inspection  |  - Reviewers evaluate draft using Checklists (Sec 1).
|                       |  - Log findings in reviews/ directory.
+-----------+-----------+
            |
            v
+-----------------------+
| 3. Revision & Commit  |  - Author resolves findings in codebase.
|                       |  - Commits updates using prefix conventions.
+-----------+-----------+
            |
            v
+-----------------------+
|  4. Final Sign-off   |  - QA Lead, Architect, and Supervisor sign the log.
|                       |  - Status changes to APPROVED.
+-----------+-----------+
            |
            v
+-----------------------+
|   5. PR Integration   |  - PR is merged into develop branch.
|                       |  - develop merges to main; release is tagged.
+-----------------------+
```
