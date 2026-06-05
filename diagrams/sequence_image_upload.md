# Sequence Diagram - Image Upload and Classification Flow
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** UML Sequence  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## Runtime Communication Sequence

```mermaid
sequenceDiagram
    participant User as Doctor or Radiologist
    participant Browser as Browser UI
    participant API as Backend API
    participant AI as AI Engine
    participant DB as SQLite DB
    participant FS as File Storage

    Note over User,FS: Phase 1 - Authentication
    User ->> Browser: Enter email and password
    Browser ->> API: POST /api/auth/login
    activate API
    API ->> DB: SELECT user WHERE email
    DB -->> API: User record and password hash
    API ->> API: Verify PBKDF2 hash
    API -->> Browser: 200 OK with token and role
    deactivate API
    Browser ->> Browser: Store JWT in session storage
    Browser -->> User: Redirect to Dashboard

    Note over User,FS: Phase 2 - DICOM Upload
    User ->> Browser: Drag DICOM file onto dropzone
    Browser ->> API: POST /api/images/upload multipart
    activate API
    API ->> API: Validate DICOM header signatures
    API ->> API: Extract metadata PatientID and Modality
    API ->> FS: Save raw dcm file
    API ->> API: Normalize pixels to PNG
    API ->> FS: Save preprocessed PNG
    API ->> DB: INSERT INTO images with patient_id and paths
    DB -->> API: image_id 142
    API -->> Browser: 201 Created with image_id and png_url
    deactivate API
    Browser -->> User: Render PNG thumbnail in canvas

    Note over User,FS: Phase 3 - AI Inference
    User ->> Browser: Click Analyze Image
    Browser ->> API: GET /api/predictions/142
    activate API
    API ->> FS: Read PNG file array
    API ->> AI: Trigger inference with normalized tensors
    activate AI
    AI ->> AI: Forward-pass through CNN layers
    AI ->> AI: Softmax activation for confidence scores
    AI ->> AI: Extract bounding box coordinates
    AI -->> API: disease type confidence and bounding boxes
    deactivate AI
    API ->> DB: INSERT INTO results
    DB -->> API: result_id 87
    API -->> Browser: 200 OK with predictions
    deactivate API
    Browser -->> User: Draw bounding box overlays and confidence

    Note over User,FS: Phase 4 - Report Sign-Off
    User ->> Browser: Add clinical notes and click Sign Off
    Browser ->> API: POST /api/reports/export
    activate API
    API ->> API: Validate Doctor role via JWT middleware
    API ->> DB: SELECT results WHERE image_id 142
    DB -->> API: Prediction data
    API ->> API: Assemble HTML template with patient and AI data
    API ->> API: Compile locked PDF via ReportLab
    API ->> FS: Save Report 142 Signed pdf
    API ->> DB: INSERT INTO reports with is_finalized TRUE
    DB -->> API: report_id 58
    API -->> Browser: 200 OK with report_id and pdf_url
    deactivate API
    Browser -->> User: Show Report Ready and download link
```

---

> [!NOTE]
> This diagram is rendered via Mermaid.js. For print/export, save as `sequence_image_upload.png`.
