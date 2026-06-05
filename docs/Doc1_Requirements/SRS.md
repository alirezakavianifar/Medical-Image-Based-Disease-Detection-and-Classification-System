# Software Requirements Specification (SRS)
## Medical Image-Based Disease Detection and Classification System

---

## 1. Introduction

### 1.1 Purpose
This Software Requirements Specification (SRS) document defines the complete functional, non-functional, interface, and safety requirements for the **Medical Image-Based Disease Detection and Classification System**. The purpose of this system is to provide automated detection and classification of pathological conditions from medical imaging inputs to assist clinical workflows and radiologists.

### 1.2 Document Audience
This document is structured to serve several key stakeholders, each focusing on specific sections:
- **Client / Hospital Representative:** Reviews the document to ensure that system features, clinical objectives, and operational constraints are fully aligned with the clinical environment.
- **Project Supervisor:** Audits the requirements for academic rigor, standards compliance, and compliance with the project plan.
- **Development Team:** Refers to functional and system interface specifications to implement the system database, API endpoints, user interfaces, and model pipelines.
- **Quality Assurance (QA) / Testing Team:** Uses the requirements as the baseline for designing unit tests, integration tests, and validating the final system outputs.

### 1.3 Intended Objectives
The system aims to achieve the following core objectives:
- **Clinical Decision Support:** Offer automated, secondary review assistance to radiologists and physicians to reduce diagnosis error rates.
- **Efficiency Enhancement:** Decrease the average time required to review medical scans and generate diagnostic reports.
- **Robust Medical Classification:** Deliver high-accuracy, multi-class disease classification (e.g., distinguishing between normal tissue, benign tumors, and malignant lesions) from medical images (e.g., MRI, CT, X-Ray scans).
- **Standards-Compliant Data Management:** Integrate with standard clinical formats (e.g., DICOM) to ensure interoperability and secure data sharing.

### 1.4 Scope of System
- **In-Scope:**
  - Secure uploading and parsing of standard medical image files (primarily DICOM formats).
  - Preprocessing of raw images (e.g., resizing, normalization, noise reduction).
  - Execution of deep learning classifiers to detect specific pathological features.
  - Interactive doctor/radiologist dashboard showing disease classification results, confidence scores, and bounding boxes around detected regions.
  - Automated PDF report generation with doctor sign-off capabilities.
  - Role-based user authentication and access control (Administrator, Doctor, Radiologist).
- **Out-of-Scope:**
  - Real-time video/ultrasound streaming analysis.
  - Direct write-back integrations into hospital PACS (Picture Archiving and Communication Systems) or EHR (Electronic Health Records) databases (this is treated as a separate enterprise middleware concern).
  - General patient billing and hospital management workflows.

### 1.5 Definitions, Acronyms, and Abbreviations

| Acronym / Term | Definition |
| :--- | :--- |
| **SRS** | Software Requirements Specification |
| **DICOM** | Digital Imaging and Communications in Medicine (international standard for medical images) |
| **PACS** | Picture Archiving and Communication System |
| **CNN** | Convolutional Neural Network |
| **AI** | Artificial Intelligence |
| **QA** | Quality Assurance |
| **UML** | Unified Modeling Language |
| **EHR** | Electronic Health Record |
| **mIoU** | Mean Intersection over Union (a common semantic segmentation evaluation metric) |
| **OA** | Overall Accuracy |

### 1.6 References
1. **IEEE Std 830-1998:** IEEE Recommended Practice for Software Requirements Specifications.
2. **DICOM Standard (PS3):** NEMA Digital Imaging and Communications in Medicine Committee.
3. **ISO 13485:** Medical devices — Quality management systems — Requirements for regulatory purposes.
4. **Project Master Plan:** [plan.md](../../plan.md) - Project master schedule and deliverable requirements.
5. **Documentation Standards:** [Documentation_Standards.md](../Documentation_Standards.md) - Naming conventions and style guidelines.

---

## 2. Overall Description

### 2.1 Product Perspective
The Medical Image-Based Disease Detection and Classification System operates as an autonomous web-based platform with a dedicated deep-learning inference backend. The system is designed to interface with DICOM source images, preprocess the visual payloads, feed them to a localized AI analysis server, and display output classification parameters on an interactive clinical dashboard.

```mermaid
graph TD
    PACS[Hospital PACS / local files] -->|Upload DICOM| WebApp[Web Application Front-end]
    WebApp -->|HTTP API POST /upload| Backend[Inference & Control Backend]
    Backend -->|Raw Images| DLModel[AI Classification Engine]
    DLModel -->|Disease Class & Bounding Boxes| Backend
    Backend -->|JSON Prediction Data| WebApp
    Backend -->|Save Metadata| SQLite[(SQLite Database)]
```

### 2.2 Product Functions
The high-level capabilities of the system are categorized as follows:
- **User Authentication and Administration:** Secure role-based login, session verification, and account profile controls.
- **Image Importation and Preprocessing:** Reading multi-frame or single-frame DICOM slices, extracting patient metadata headers, and applying spatial rescaling, contrast adjustment, and noise filtering.
- **Disease Area Detection:** Identifying bounding regions of pathological interest (e.g., lesions, tumors, fractures) and overlaying heatmap/bounding-box visual markers.
- **Disease Multi-Class Classification:** Assisting diagnostic analysis by classifying scans into distinct clinical labels (e.g., Normal, Benign, Malignant) accompanied by statistical confidence levels.
- **Dashboard Reporting & Audit trail:** Presenting visual overlays side-by-side with Patient IDs, demographic records, and confidence statistics.
- **Diagnostic Exporting:** Building formatted summary reports in PDF format containing physician comments and signature fields.

### 2.3 User Classes and Characteristics
- **Administrators:** Responsible for system maintenance, user registration control, database backup, audit log review, and configuring system security levels.
- **Radiologists:** Heavy-use clinical staff who upload scan archives, trigger model executions, examine visual bounding boxes, and formulate diagnosis drafts.
- **Doctors:** Clinical recipients who retrieve cases, review the classification results and radiologists' notes, add final diagnosis annotations, and approve PDF reports.

### 2.4 Operating Environment
- **Server Infrastructure:**
  - **Operating System:** Ubuntu 22.04 LTS or compatible server OS.
  - **Runtime Runtime:** Python 3.10+ with PyTorch/TensorFlow.
  - **Database:** SQLite for lightweight local caching, or PostgreSQL for enterprise-grade deployments.
  - **Hardware acceleration:** NVIDIA CUDA-enabled GPU with >= 8GB VRAM.
- **Client Interface:**
  - Standard modern web browsers (Chrome 110+, Edge 110+, Firefox 105+, Safari 16+).
  - Responsive layout designed for desktop display resolutions (>= 1280x720).

### 2.5 Design and Implementation Constraints
- **Regulatory Compliance:** Must adhere to data isolation and privacy mandates under HIPAA (Health Insurance Portability and Accountability Act) and GDPR.
- **Image Dimensionality Limits:** Maximum size of uploaded DICOM batches is capped at 100MB per session to prevent backend memory overflows.
- **Latency Boundaries:** Deep learning inference execution must compile and return scores within 5 seconds of the image upload completion.
- **Accessibility:** Text elements and UI layouts must satisfy WCAG 2.1 AA web accessibility guidelines.

### 2.6 Assumptions and Dependencies
- **Data Integrity:** Uploaded medical images are assumed to conform to the standard DICOM metadata specifications without header corruption.
- **Active Connection:** The system assumes constant backend availability and network connectivity for transferring image payloads from the web application interface.
- **Pre-trained Weights:** The system depends on pre-trained neural network weights being correctly mounted and loaded into host VRAM at server startup.

---

## 3. Functional Requirements

### 3.1 User Authentication & Session Management (FR-01)
- **Description:** Enforce credentials verification and session management to secure access to clinical data based on user roles (Admin, Doctor, Radiologist).
- **Inputs:** 
  - Login payload: Email Address, Plaintext Password.
  - Session cookie / Authorization header token.
- **Processing:** 
  - Retrieve user record by Email Address; compute PBKDF2 password verification.
  - Generate JWT (JSON Web Token) with user role metadata upon verification success.
  - Establish a secure, HTTP-only session cookie.
  - Enforce role middleware validation before routing clinical API requests.
- **Outputs:**
  - Success: User session token, redirect routing parameters to dashboard interface.
  - Failure: Display of localized authentication error message (invalid credentials).

### 3.2 DICOM Image Upload & Parsing (FR-02)
- **Description:** Provide interfaces to import standard medical scans, validate file headers, and extract metadata fields.
- **Inputs:** 
  - Image Payload: DICOM formatted file (.dcm) containing metadata and pixel array.
- **Processing:** 
  - Read binary header signatures to verify compliance with the DICOM standard.
  - Extract Patient ID, Patient Name, Scan Date, Modality, and Manufacturer details.
  - Compress pixel payload to high-quality lossy JPEG or lossless PNG format for web rendering.
  - Store parsed metadata in the SQLite database and raw files in secure local storage.
- **Outputs:**
  - Visual toast representing file status (uploaded successfully).
  - New DB record created with a unique Image ID.
  - Preprocessed thumbnail image rendered in the client view.

### 3.3 AI Image Classification & Inference (FR-03)
- **Description:** Execute convolutional neural network (CNN) model pipeline to evaluate scan features, output disease classes, and locate anomalous regions.
- **Inputs:** 
  - Normalized tensor array from the uploaded image.
  - Request parameter: Active Image ID.
- **Processing:** 
  - Rescale image array to match model input dimensions (e.g. 224x224 or 512x512 pixels).
  - Forward-pass image array through the AI detection layer.
  - Retrieve raw logit outputs and compute softmax activation to get confidence percentages.
  - Calculate spatial coordinate bounding boxes enclosing abnormal structures.
- **Outputs:**
  - Predicted category (e.g., Pneumonia, Brain Tumor, Normal).
  - Confidence metric score (e.g., 96.4%).
  - Bounding box coordinates array.

### 3.4 Diagnosis Results Dashboard Display (FR-04)
- **Description:** Display parsed metadata, prediction details, and scan visuals with overlay bounding boxes side-by-side.
- **Inputs:** 
  - Current Image ID, matching patient data, AI prediction labels, and confidence metrics.
- **Processing:** 
  - Retrieve medical record and spatial overlays matching the Image ID.
  - Construct canvas elements overlaying spatial bounding boxes on top of the preprocessed image.
  - Format confidence ratios into graphical bar progress indicators.
- **Outputs:**
  - Single-page view with metadata panel, prediction panel, and interactive medical image viewer canvas.

### 3.5 Medical Diagnostic PDF Export (FR-05)
- **Description:** Format medical findings, AI outputs, and doctor annotations into a downloadable, locked PDF file.
- **Inputs:** 
  - Active Patient Record, model outputs, doctor written feedback, doctor signature status.
- **Processing:** 
  - Assemble metadata, image files, classification label, confidence score, and doctor notes into an HTML-styled page template.
  - Run the PDF compile library to produce a standard document representation.
  - Save the PDF path in the database and block modifications to the report.
- **Outputs:**
  - Downloadable PDF document containing the patient case summary and diagnostic outcomes.

---

## 4. Non-Functional Requirements

### 4.1 Performance Requirements
- **Execution Speed:** Neural network classification pipeline must complete model execution in under 5.0 seconds from the upload submit action.
- **UI Responsiveness:** Page navigation operations and API queries (excluding model inference) must respond in under 1.0 second.
- **Throughput:** The database must support up to 50 concurrent sessions without connection timeouts or latency drops.

### 4.2 Security & Privacy Requirements
- **Transmission Security:** All external web and API client traffic must be encrypted using Transport Layer Security (TLS 1.3) over HTTPS.
- **Data Protection at Rest:** Clinical databases and raw DICOM assets must be encrypted on physical host filesystems using AES-256.
- **Automatic Timeout:** User dashboard sessions must automatically terminate after 15 minutes of user inactivity.
- **Role Isolation:** Only verified Doctors may modify clinical notes or sign off on final diagnostic PDF exports.

### 4.3 Reliability & Availability
- **System Uptime:** The system dashboard must achieve an annual uptime percentage of 99.9% (excluding scheduled maintenance).
- **Graceful Failure:** Model server crashes or out-of-memory errors must not affect the main database or disconnect the user's active session.

### 4.4 Interoperability & Portability
- **Clinical Integration:** The system must accept DICOM standard PS3 compliance files across multiple modalities (CT, MRI, X-Ray).
- **Client Portability:** The user interface must maintain full layout rendering compatibility across Chrome, Safari, and Edge.

---

## 5. External Interface Requirements

### 5.1 User Interfaces
- **Login Screen:** Provides text input fields for Email, Password, and login submissions with field validations.
- **Main Dashboard Panel:**
  - **Left Sidebar:** User status, file uploads, patient lists.
  - **Center Viewer:** Interactive canvas showing DICOM scan and spatial bounding boxes.
  - **Right Sidebar:** Case details, AI classification confidence scores, doctor clinical logs, and report export action button.

### 5.2 Hardware Interfaces
- **GPU Accelerator:** Enforces minimum 8GB VRAM NVIDIA CUDA-capable graphics card for deep learning inference.
- **Host Memory:** Minimum 16GB system RAM on the server node.
- **Persistent Storage:** Minimum 1TB NVMe storage arrays.

### 5.3 Software Interfaces
- **Python Libraries:** Pydicom (DICOM file parsing), PyTorch/TensorFlow (ML inference), ReportLab (PDF compilation).
- **Database Engine:** SQLite runtime interface for caching.

### 5.4 API & Communication Interfaces
- **API Protocol:** RESTful HTTP endpoints using JSON format.
- **Primary Routes:**
  - `POST /api/auth/login`: Authenticate users.
  - `POST /api/images/upload`: Upload DICOM files.
  - `GET /api/predictions/{image_id}`: Fetch diagnosis scores and coordinates.
  - `POST /api/reports/export`: Generate and lock the PDF report.
