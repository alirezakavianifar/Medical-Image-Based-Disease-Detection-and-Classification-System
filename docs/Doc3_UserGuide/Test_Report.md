# Quality Assurance Verification & Test Report
## Medical Image-Based Disease Detection and Classification System

---

## 1. Test Strategy & Scope

This document details the verification plan and execution results used to validate the functional capabilities, non-functional performance boundaries, and safety constraints of the **Medical Image-Based Disease Detection and Classification System**.

### 1.1 Test Scope Boundaries
- **In-Scope Testing:** User authentication roles logic, DICOM upload handlers, PyTorch classification inference correctness, Canvas visual bounding box rendering, doctor text note inputs, and finalized PDF report generation.
- **Out-of-Scope Testing:** Direct hospital PACS connections performance, multi-user stress testing beyond 100 concurrent sessions, and raw deep learning training convergence verification.

### 1.2 Verification Environment & Tools
- **Test Server Host:** Ubuntu 22.04 LTS, NVIDIA RTX 3080 GPU (10GB VRAM), CUDA 12.1, SQLite 3.37.
- **Testing Tools:**
  - `cURL` and `Postman` for HTTP REST API endpoint verification.
  - Manual verification on browser clients (Chrome 118, Safari 17).
  - Automation scripts using Python's built-in `unittest` library for database transaction checks.

---

## 2. Test Case Specifications

### 2.1 TC01: User Login Authentication
- **Test Description:** Validate that users can securely authenticate and obtain JWT tokens.
- **Test Type:** Functional, Positive.
- **Inputs:** 
  - Email: `doctor_john@hospital.org`
  - Password: `ClinicalPassword123`
- **Execution Steps:**
  1. Open login view interface.
  2. Input Email and Password.
  3. Click "Sign In".
- **Expected Result:** HTTP 200 OK status returned containing JWT token payload. Browser sets authorization cookies and redirects the client to the clinical dashboard workspace.

### 2.2 TC02: DICOM Image Upload & Parsing
- **Test Description:** Validate that raw DICOM files are accepted, metadata is parsed, and visual PNGs are cached.
- **Test Type:** Functional, Positive.
- **Inputs:** 
  - Standard compliant DICOM `.dcm` chest scan (12MB).
- **Execution Steps:**
  1. Login as Radiologist.
  2. Open Upload panel.
  3. Drag file onto dropzone.
- **Expected Result:** HTTP 201 Created returned. Upload progress indicator reaches 100%. Raw file is saved to storage, and a preprocessed PNG representation is rendered in the viewer canvas.

### 2.3 TC03: AI Inference Prediction Execution
- **Test Description:** Validate that the AI engine completes classification and outputs bounding box coordinates.
- **Test Type:** Functional, Positive.
- **Inputs:** 
  - Target Image ID: `142` (uploaded scan).
- **Execution Steps:**
  1. Select Case 142.
  2. Click "Analyze Image".
- **Expected Result:** HTTP 200 OK returned in under 5.0 seconds. Dashboard displays the predicted disease category label, confidence percentage indicator, and draws a translucent bounding box overlay on the viewer canvas.

### 2.4 TC04: Role-Based Authorization Guard (Negative Test)
- **Test Description:** Ensure users with non-Doctor roles cannot compile and finalize signed reports.
- **Test Type:** Security, Negative.
- **Inputs:** 
  - User: Radiologist account session.
  - Action: Trigger report final sign-off.
- **Execution Steps:**
  1. Login as Radiologist.
  2. Open Case 142 results view.
  3. Input notes and click "Sign Off & Lock Case".
- **Expected Result:** HTTP 403 Forbidden status returned. Client dashboard displays an access denied warning banner. The case record remains in draft mode.

### 2.5 TC05: Upload Size Boundary Limit (Negative Test)
- **Test Description:** Ensure files exceeding the size boundary limit are rejected.
- **Test Type:** Boundary, Negative.
- **Inputs:** 
  - Large file: `dummy_scan.dcm` (110MB).
- **Execution Steps:**
  1. Drag and drop file onto dropzone container.
- **Expected Result:** Upload process is blocked immediately. A red validation toast notifies the user: *File size exceeds 100MB limit*. No backend API transfer is triggered.

---

## 3. Test Execution Summary

The verification suite was executed against release candidate `v1.0.0-RC`.

| Test ID | Title | Test Category | Execution Status | Result | Notes |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **TC01** | User Login Authentication | Functional | Executed | **PASS** | JWT session token successfully generated. |
| **TC02** | DICOM Image Upload | Functional / File IO | Executed | **PASS** | Metadata successfully cached in SQLite. |
| **TC03** | AI Inference Execution | Performance / AI | Executed | **PASS** | Inference finished in 1.45 seconds. |
| **TC04** | Role-Based Authorization Guard | Security | Executed | **PASS** | Endpoint blocked non-Doctor access. |
| **TC05** | Upload Size Boundary Limit | Boundary | Executed | **PASS** | File rejected locally at the browser level. |

### 3.1 Execution Metrics
- **Total Test Cases:** 5
- **Total Executed:** 5
- **Passed:** 5
- **Failed:** 0
- **Test Success Rate:** **100.0%**

---

## 4. Historical Defect Logs

The following defects were identified during early integration testing and verified as resolved in the final execution run:

### 4.1 Defect 01: Client UI Bypass on Sign-Off Endpoint
- **Severity:** High
- **Description:** A Radiologist could bypass frontend UI disablements and successfully POST to `/api/reports/export` by sending requests directly using Postman.
- **Resolution:** Implemented role-based verification middleware checks on the backend endpoint. Direct API requests now correctly return `403 Forbidden` for non-Doctor accounts. verified resolved via TC04.

### 4.2 Defect 02: Inference Latency OOM Crash
- **Severity:** Medium
- **Description:** Launching the backend with multiple uvicorn server workers caused GPU out-of-memory crashes as multiple processes attempted to mount model weights into VRAM.
- **Resolution:** Configured the deployment configuration to lock work threads count to 1 (`--workers 1`) and preloaded weights into unified VRAM during server boot. Verified resolved via TC03.
