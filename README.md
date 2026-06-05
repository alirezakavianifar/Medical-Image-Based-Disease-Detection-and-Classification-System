# Medical Image-Based Disease Detection and Classification System

This repository hosts the documentation, design models, process specifications, and version control workflows for the **Medical Image-Based Disease Detection and Classification System**. 

The main objective of this project is to implement a professional, standardized Software Engineering lifecycle through comprehensive artifacts, structured reviews, and strict version control.

---

## 📂 Repository Structure

The project layout is structured as follows:

```text
Medical-Image-Based-Disease-Detection-and-Classification-System/
├── docs/
│   ├── Doc1_Requirements/   # Software Requirements Specification (SRS) documents
│   ├── Doc2_Design/         # Software Design Document (SDD) & diagrams
│   ├── Doc3_UserGuide/      # User, Installation, and Test manuals/reports
│   └── Final_Report/        # Final project analysis and deliverables report
├── diagrams/                # Raw diagram files (UML, workflows, mockups)
├── templates/               # Reusable templates for requirements and designs
├── reviews/                 # Peer review notes and document inspection logs
├── plan.md                  # The master step-by-step project plan
└── README.md                # This project readme file
```

### Directory Descriptions
- **`docs/Doc1_Requirements/`**: Contains the Software Requirements Specification (SRS) structured under IEEE 830 standards.
- **`docs/Doc2_Design/`**: Contains the Software Design Document (SDD), which specifies the architecture, data models, API endpoints, and UML diagrams.
- **`docs/Doc3_UserGuide/`**: Houses user manual instructions, system setup/installation requirements, and QA test execution reports.
- **`docs/Final_Report/`**: Holds the comprehensive project completion report.
- **`diagrams/`**: Stores visual assets (e.g., SVG, PNG, or Mermaid files) for architecture, databases, and use case diagrams.
- **`reviews/`**: Documents peer approvals, checklists, and review results.

---

## 🪵 Git Branch & Versioning Strategy

This project enforces a structured branching model to ensure quality control:

### 1. Main Branches
- **`main`**: The production-ready branch containing only fully approved, finalized documents.
- **`develop`**: The integration branch where all finished phase-level drafts are consolidated and tested.

### 2. Feature & Phase Branches
For each documentation phase, a dedicated feature branch is checked out from `develop`:
- `doc1-requirements` for SRS drafting and review.
- `doc2-design` for SDD and UML architecture design.
- `doc3-userguide` for user manuals and QA test logs.
- `final-report` for final project reporting.

### 3. Review & Pull Request Workflow
1. Work is committed to the phase-specific branch.
2. A Pull Request (PR) is opened targeting `develop`.
3. After a peer review checklist is completed in the `reviews/` directory, the PR is merged into `develop`.
4. Finalized versions are merged from `develop` into `main` and tagged using semantic tagging conventions:
   - `v1.0-SRS` for approved Requirements.
   - `v1.0-SDD` for approved System Designs.
   - `v1.0-DOC3` for User Guides and Test Reports.
   - `v1.0-FINAL` for the final delivery package.

---

## 🚀 Getting Started

Since this project focus is on **documentation and process lifecycle management**:
- Navigation: Review the files inside `docs/` using a markdown viewer or PDF editor.
- Master Plan: Refer to [plan.md](plan.md) to see the execution status and timeline of milestones.
- Verification: See the verification checklist within each document phase.
