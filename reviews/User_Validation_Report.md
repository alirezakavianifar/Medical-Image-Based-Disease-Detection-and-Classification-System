# Clinical User & System Deployment Validation Report

| Parameter | Details |
| :--- | :--- |
| **Document Evaluated** | User Guide, Installation Guide, Test Manual Suite (`Index.md`) |
| **Active Version** | `v1.0.0` (Draft for Validation) |
| **Validation Date** | June 5, 2026 |
| **Verification Lead** | Lead Quality Assurance Engineer |

---

## 1. Overview & Validation Strategy

The objective of this verification phase is to validate that the User Manual and Installation Guide are clear, comprehensive, and reproducible for their respective target audiences.
To execute this, validation team members were assigned specific roles to walk through the guides:
1. **Clinical Role Play:** A validator acting as a **Doctor / Radiologist** executed UI tasks using only the [User_Manual.md](../docs/Doc3_UserGuide/User_Manual.md) as reference.
2. **Deployment Role Play:** A validator acting as a **System Administrator** executed CLI setup tasks using only the [Installation_Guide.md](../docs/Doc3_UserGuide/Installation_Guide.md) as reference.

---

## 2. Clinical User Manual Validation (Role Play)

### 2.1 Tasks Executed
- Secure login and verification of role routing.
- Uploading a standard `.dcm` DICOM image file.
- Inspecting preprocessed visual scan displays and canvas bounding box coordinates overlays.
- Navigating contrast/brightness controls to enhance scan details.
- Entering clinical annotations, signing off reports, and downloading PDF files.

### 2.2 Evaluation Results
- **Pass Rate:** **100%**
- **Findings:** The manual's layout matches the browser views. Instructions for canvas drawing controls zoom/contrast were clear. Bounding box coordinates representations were easy to interpret.

---

## 3. Server Installation Guide Validation (Role Play)

### 3.1 Tasks Executed
- Setting up folder repositories, initializing Python virtual environments (`venv`), and installing library dependencies using pip.
- Configuring environment variables in the `.env` file.
- Executing SQLite database migration scripts (`init_db.py`) to build tables and indices.
- Mounting PyTorch weights and starting uvicorn backend servers.
- Querying health routing endpoints using `cURL` CLI tools.

### 3.2 Evaluation Results
- **Pass Rate:** **100%**
- **Findings:** CLI scripts compiled without dependency warnings. Database schema creation script initialized schemas correctly. Health checks confirmed operational statuses.

---

## 4. Feedback Loop & Documentation Adjustments Log

The following feedback comments collected during role-play validation walkthroughs were addressed in the final manuals drafts:

### 4.1 UI Upload Warning Note
- **Feedback:** Radiologists noted that users might attempt to upload non-compliant files, causing unnecessary upload latency before a backend format check occurs.
- **Adjustment:** Appended warning notes in Section 3 of [User_Manual.md](../docs/Doc3_UserGuide/User_Manual.md) specifying that browser-side checks inspect file extensions locally before beginning backend API transfers.

### 4.2 Uvicorn Worker Thread Limits
- **Feedback:** System Administrators noted that starting uvicorn with default multiple processes (`--workers`) caused CUDA runtime processes conflicts on single-GPU servers.
- **Adjustment:** Added configuration notes in Section 5.2 of [Installation_Guide.md](../docs/Doc3_UserGuide/Installation_Guide.md) to explicitly set the process threads limit to 1 worker (`--workers 1`) on standard GPU setups.

---

## 5. Final Validation Sign-off

The Phase 4 documentation suite (User, Installation, and Test Guides) has successfully resolved all validation findings and is hereby **APPROVED** for baseline.

| Stakeholder Role | Name / Signature | Status | Date |
| :--- | :--- | :---: | :--- |
| **Lead QA Engineer** | *QA Validation Committee* | **APPROVED** | June 5, 2026 |
| **Lead Developer** | *Development Team Lead* | **APPROVED** | June 5, 2026 |
| **Project Supervisor** | *Supervisor Review Panel* | **APPROVED** | June 5, 2026 |
| **Client Representative** | *Hospital Clinical Advisory* | **APPROVED** | June 5, 2026 |
