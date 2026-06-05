# Software Design Document (SDD)
## Medical Image-Based Disease Detection and Classification System

---

## 1. Introduction

### 1.1 Purpose
This Software Design Document (SDD) provides a comprehensive description of the architectural design, component decomposition, database structure, and external interfaces for the **Medical Image-Based Disease Detection and Classification System**. It translates the requirements outlined in the Software Requirements Specification (SRS) into structured technical blueprints for implementation.

### 1.2 Document Audience
This document is designed for the following technical stakeholders:
- **System Developers:** To implement modular backend interfaces, construct model execution pipelines, design database adapter structures, and build front-end layouts.
- **Quality Assurance (QA) / Testers:** To design detailed test integration suites, trace code components back to requirements, and run component validations.
- **System Administrators:** To understand deployment environments, network protocols, server GPU setups, and data security dependencies.
- **Project Supervisor:** To verify system design feasibility, compliance with documentation standards, and architectural completeness.

### 1.3 Scope of Design
The design specifications cover:
- Layered architectural boundaries (Presentation Layer, Application Logic Layer, AI Model Inference Layer, and Persistence Layer).
- Modular decomposition of system features (Authentication, DICOM Parsing, Neural Network classification, Canvas Rendering, and PDF report compilation).
- UML Design models showing workflows, actors, class behaviors, and execution sequences.
- Relational database schema structure.
- REST API endpoint contracts and JSON schema payload formats.

---

## 2. System Component Decomposition

To satisfy the functional requirements (FR-01 to FR-05) defined in the SRS, the system is decomposed into six main functional modules:

```text
+-------------------------------------------------------------+
|                     Presentation Layer                      |
|  - Login View      - Case List View     - Clinical Canvas   |
+------------------------------+------------------------------+
                               | API Requests (HTTPS)
                               v
+-------------------------------------------------------------+
|                  Application Logic Layer                    |
|  - Auth Controller              - Image Manager Controller  |
|  - Report Compiler Module       - Database Adapter          |
+--------------------+---------------------+------------------+
                     |                     |
   Tensors via NumPy v                     v DB Operations
+--------------------------+    +-----------------------------+
|    AI Inference Layer    |    |      Persistence Layer      |
|  - Model Loader Node     |    |  - SQLite Database Engine   |
|  - Classification Pipeline|   |  - DICOM File System Cache  |
+--------------------------+    +-----------------------------+
```

### 2.1 Presentation Component (Client Interface)
- **Role:** Handles rendering the browser viewport and managing asynchronous client-side routing.
- **Sub-modules:**
  - *Authentication Panel:* Interface for email/password credentials input and session storage.
  - *Patient Archive Panel:* Lists uploaded case metadata matching user filter parameters.
  - *Interactive Canvas Viewer:* Draws the raw preprocessed medical scan and maps bounding box coordinates visually.
  - *Diagnosis Control Hub:* Panel containing clinical logs, confidence ratings, and diagnostic export controls.

### 2.2 Authentication & Access Control Module
- **Role:** Authenticates user credentials, generates JSON Web Tokens (JWT), and checks route permission roles.
- **Sub-modules:**
  - *Credentials Verifier:* Manages password hashing verification using PBKDF2.
  - *Token Controller:* Issues, decodes, and checks expiration of JWT session tokens.
  - *Middleware Guard:* Enforces clinical path restrictions (e.g. preventing Radiologists from signing final reports).

### 2.3 Image Importation & Storage Manager
- **Role:** Handles file system upload processes, DICOM file validation, header parsing, and cache allocation.
- **Sub-modules:**
  - *DICOM Header Parser:* Extracts tags (Patient ID, Study Date, Modality) using `pydicom`.
  - *Preprocessing Normalizer:* Converts pixel arrays to normalized float matrices for model compatibility, and compresses raw pixels to PNG formats for web client presentation.
  - *Cache Manager:* Allocates local disk storage for DICOM binaries.

### 2.4 AI Model Inference Engine
- **Role:** Manages ML model lifecycle, runs inference checks on preprocessed tensors, and maps spatial anomaly areas.
- **Sub-modules:**
  - *Model Loader:* Mounts pre-trained network model weights into GPU memory at server startup.
  - *Inference Classifier:* Runs forward-pass operations and maps logits using softmax.
  - *Spatial Analyzer:* Calculates pixel coordinate arrays corresponding to anomalous regions.

### 2.5 Report Compiler Module
- **Role:** Assembles diagnostic summaries, doctor notes, and visual findings into a locked PDF format.
- **Sub-modules:**
  - *Template Engine:* Assembles layout variables into standardized markup.
  - *PDF Generator:* Compiles text and images to PDF binaries using `ReportLab`.
  - *Locker Module:* Tags DB records as finalized and disables further editing.

### 2.6 Persistence & DB Adapter
- **Role:** Abstracts data operations through structured queries.
- **Sub-modules:**
  - *User Schema Manager:* Manages database profiles, password hashes, and access permissions.
  - *Image Metadata Manager:* Handles Patient IDs, dates, file locations, and status records.
  - *Results Schema Manager:* Manages category tags, confidence levels, and coordinate outputs.
