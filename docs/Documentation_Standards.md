# Documentation & Process Standards Guide

This document defines the standards, conventions, workflows, and protocols used across the **Medical Image-Based Disease Detection and Classification System** repository.

---

## 1. File Naming Conventions

To maintain a clean and easily navigable repository, all files must adhere to the following naming conventions:

### 1.1 Master Source Files (Markdown)
All master documentation files must be written in Markdown (`.md`) format using snake_case or specific standard abbreviations, starting with uppercase letters:
- **Project Charter:** `Project_Charter.md`
- **Requirements (SRS):** `SRS.md`
- **System Design (SDD):** `SDD.md`
- **User Guide:** `User_Guide.md`
- **Installation Guide:** `Installation_Guide.md`
- **Test Report:** `Test_Report.md`
- **Final Report:** `Final_Report.md`

### 1.2 Exported Artifacts (PDF/DOCX)
When exporting static documents for external reviews, supervisor evaluation, or client presentations, append the release version number using semantic formatting:
- **Format:** `{DocType}_v{Major}.{Minor}.{Patch}.{extension}`
- **Examples:**
  - `SRS_v1.0.0.pdf`
  - `SDD_v1.0.0.docx`
  - `UserGuide_v1.2.0.pdf`

### 1.3 Diagram Assets
Raw and exported diagram assets (stored in `diagrams/`) must follow lower_snake_case and specify the type of diagram:
- **Format:** `{diagram_type}_{subject_description}.{extension}`
- **Examples:**
  - `usecase_doctor_interaction.png`
  - `sequence_image_upload.svg`
  - `class_detection_engine.png`
  - `activity_preprocess_workflow.png`

---

## 2. Formatting & Markdown Guidelines

All `.md` source documents must follow standard Markdown and GitHub Flavored Markdown (GFM) conventions to ensure consistent readability:

1. **Heading Hierarchy:** Use a single `# H1` per document for the main title. Sub-sections must follow hierarchical order: `## H2` for main headings, `### H3` for sub-sections, and `#### H4` for sub-sub-sections.
2. **Lists and Tables:** Use bulleted or numbered lists for readability. Use standard Markdown tables for comparative, structured data (e.g., test cases, project timelines).
3. **Diagram References:** Diagrams must be centered, referenced by captions, and stored in the root `diagrams/` folder. Use standard Markdown image syntax:
   `![Caption text](../../diagrams/filename.png)`
4. **Admonitions (GitHub-Style Alerts):** Use alerts strategically to call out important notes:
   - `> [!NOTE]` for extra details.
   - `> [!IMPORTANT]` for crucial system aspects.
   - `> [!WARNING]` or `> [!CAUTION]` for potential system limitations or safety/privacy-critical notes.

---

## 3. Version Numbering System

We apply a document-centric variation of Semantic Versioning (`vX.Y.Z`):

| Level | Component | Trigger Criteria |
| :--- | :--- | :--- |
| **Major** | **`X`** (e.g., `v1.0.0`) | Official baselined document releases for review phases (e.g. final SRS baseline). |
| **Minor** | **`Y`** (e.g., `v1.1.0`) | Significant additions of new sections, architectural revisions, or new diagram blocks. |
| **Patch** | **`Z`** (e.g., `v1.1.1`) | Typo fixes, minor text edits, formatting adjustments, or link corrections. |

---

## 4. Git Branching & Workflow

Development must strictly follow the staging and branch integration strategy:

1. **Primary Branches:**
   - `main`: Stores only stable, approved, and finalized versions of documents. Direct commits to `main` are prohibited.
   - `develop`: The active integration branch. Feature branches merge here after passing reviews.
2. **Phase-Specific Feature Branches:**
   - Requirements phase: `doc1-requirements`
   - Design phase: `doc2-design`
   - Guides & Testing phase: `doc3-userguide`
   - Final Reporting phase: `final-report`
3. **Integration Steps:**
   - Create a feature branch from `develop`.
   - Complete drafting/updating.
   - Submit a Pull Request (PR) from the feature branch to `develop`.
   - Conduct a peer review check (logged in the `reviews/` directory).
   - Once approved, merge the PR into `develop`.
   - When a project phase is finalized, merge `develop` into `main` and tag the release.

---

## 5. Git Commit Message Conventions

Commit messages must be concise, descriptive, and prefixed with the active phase identifier. 

### 5.1 Format
`<PREFIX>: <Action description>`

### 5.2 Prefix Reference Table
- **`DOC1:`** Software Requirements Specification (SRS) tasks.
- **`DOC2:`** Software Design Document (SDD) and diagram tasks.
- **`DOC3:`** User Manuals, Installation Guides, and Test Documentation.
- **`REPORT:`** Final Project Report tasks.
- **`INFRA:`** Repository infrastructure, `.gitignore`, directory layouts, and standards documentation.

### 5.3 Examples
- `INFRA: Added repository file structure and .gitignore`
- `DOC1: Drafted system functional requirements for MRI image upload`
- `DOC2: Added sequence diagram for disease classification API`
- `DOC3: Added installation steps for Python runtime environment`
