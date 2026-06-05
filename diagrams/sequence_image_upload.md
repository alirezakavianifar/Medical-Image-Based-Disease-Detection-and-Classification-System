# Sequence Diagram – Image Upload & Classification Flow
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** UML Sequence  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## Runtime Communication Sequence

```mermaid
sequenceDiagram
    autonumber
    actor User as 🩺 Doctor / Radiologist
    participant Browser as 🌐 Browser UI
    participant API as ⚙️ Backend API
    participant AI as 🤖 AI Engine (GPU)
    participant DB as 🗄️ SQLite DB
    participant FS as 📁 File Storage

    Note over User, FS: Phase 1 – Authentication
    User ->> Browser: Enter email & password
    Browser ->> API: POST /api/auth/login
    activate API
    API ->> DB: SELECT user WHERE email = ?
    DB -->> API: User record + password_hash
    API ->> API: Verify PBKDF2 hash
    API -->> Browser: 200 OK { token, role, name }
    deactivate API
    Browser ->> Browser: Store JWT in session storage
    Browser -->> User: Redirect to Dashboard

    Note over User, FS: Phase 2 – DICOM Upload
    User ->> Browser: Drag DICOM file onto dropzone
    Browser ->> API: POST /api/images/upload (multipart)
    activate API
    API ->> API: Validate DICOM header signatures
    API ->> API: Extract metadata (PatientID, Modality)
    API ->> FS: Save raw .dcm file
    API ->> API: Normalize pixels → PNG
    API ->> FS: Save preprocessed PNG
    API ->> DB: INSERT INTO images (patient_id, paths...)
    DB -->> API: image_id = 142
    API -->> Browser: 201 Created { image_id, png_url }
    deactivate API
    Browser -->> User: Render PNG thumbnail in canvas

    Note over User, FS: Phase 3 – AI Inference
    User ->> Browser: Click "Analyze Image" (image_id=142)
    Browser ->> API: GET /api/predictions/142
    activate API
    API ->> FS: Read PNG file array
    API ->> AI: Trigger inference (normalized tensors)
    activate AI
    AI ->> AI: Forward-pass through CNN layers
    AI ->> AI: Softmax activation (confidence scores)
    AI ->> AI: Extract bounding box coordinates
    AI -->> API: { disease_type, confidence, bounding_boxes }
    deactivate AI
    API ->> DB: INSERT INTO results (image_id, disease_type...)
    DB -->> API: result_id = 87
    API -->> Browser: 200 OK { disease_type, confidence_score, bounding_boxes }
    deactivate API
    Browser -->> User: Draw bounding box overlays + confidence %

    Note over User, FS: Phase 4 – Report Sign-Off
    User ->> Browser: Add clinical notes + click "Sign Off"
    Browser ->> API: POST /api/reports/export
    activate API
    API ->> API: Validate Doctor role (JWT middleware)
    API ->> DB: SELECT * FROM results WHERE image_id=142
    DB -->> API: Prediction data
    API ->> API: Assemble HTML template (patient + AI data + notes)
    API ->> API: Compile locked PDF (ReportLab)
    API ->> FS: Save Report_142_Signed.pdf
    API ->> DB: INSERT INTO reports (image_id, doctor_id, is_finalized=TRUE)
    DB -->> API: report_id = 58
    API -->> Browser: 200 OK { report_id, pdf_url, is_finalized: true }
    deactivate API
    Browser -->> User: Show "Report Ready" + download link
```

---

> [!NOTE]
> This diagram is rendered via Mermaid.js. For print/export, save as `sequence_image_upload.png`.
