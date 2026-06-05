# Documentation Index: User, Installation, & Testing Guides

This directory contains the user manuals, deployment installation guides, and quality assurance testing reports for the **Medical Image-Based Disease Detection and Classification System**.

To ensure clarity and targeting, the documentation suite is structured into three specialized documents based on user roles and technical responsibilities.

---

## 1. Audience & Document Mapping Matrix

| Document File | Target Audience | Focus Area | Description |
| :--- | :--- | :--- | :--- |
| **[User_Manual.md](User_Manual.md)** | Doctors, Radiologists | End-user UI workflow | Step-by-step instructions for uploading scans, reviewing classification heatmaps, writing annotations, and signing reports. |
| **[Installation_Guide.md](Installation_Guide.md)** | System Admins, DevOps, Devs | Server deployment & setup | Hardware prerequisites, python dependencies config, database migrations, GPU CUDA triggers, and startup tests. |
| **[Test_Report.md](Test_Report.md)** | QA Engineers, Supervisors, Clients | Verification & Quality Audit | Traceability matrix, detailed test cases (TC01-TC05), pass/fail logs, bug tracking, and compliance checks. |

---

## 2. Table of Contents & Outline Specifications

### 2.1 User Manual Outline
- **1. Introduction & Dashboard Layout**
- **2. Authentication Procedures** (Secure Login, role-based view limits, auto-timeout)
- **3. Medical scan Uploading** (Single file imports, DICOM header validations, batch processing status)
- **4. Clinical Result Interpretation** (Visual canvas overlay review, bounding boxes, category tags, and confidence scores)
- **5. Case Finalization & Report Export** (Drafting notes, signature approvals, and downloading locked PDF reports)

### 2.2 Installation Guide Outline
- **1. Deployment Requirements** (OS version, RAM bounds, GPU VRAM limits, Python 3.10+ dependencies)
- **2. Environment Configuration** (Checkout codebase, create python virtual environment, install packages)
- **3. Persistence & Database Initialization** (SQLite cache setup, table structures migrations)
- **4. AI Engine Mounting** (Downloading pre-trained CNN neural weights, CUDA acceleration binding)
- **5. Launch & Verify** (Start backend and frontend nodes, run basic connection tests)

### 2.3 Test Report Outline
- **1. Test Strategy & Scope** (Scope boundaries, test tools, verification environments)
- **2. Test Case Matrix** (Detailed inputs, expected results, and trace requirements for TC01 to TC05)
- **3. Execution Records & Metrics** (Pass/Fail percentages, test log records)
- **4. Defect Logs & Resolutions** (Bug logs, tracking status, corrective actions, and QA sign-offs)
