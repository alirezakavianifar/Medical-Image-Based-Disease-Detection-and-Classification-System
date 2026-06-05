# Activity Diagram - Image Processing Workflow
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** Activity / Workflow  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## End-to-End Clinical Workflow

```mermaid
flowchart TD
    classDef startEnd fill:#1a73e8,stroke:#0d47a1,color:#ffffff
    classDef process fill:#e3f2fd,stroke:#1a73e8,color:#0d47a1
    classDef decision fill:#fff8e1,stroke:#f9a825,color:#4a3000
    classDef database fill:#e8f5e9,stroke:#2e7d32,color:#1b5e20
    classDef error fill:#fce4ec,stroke:#c62828,color:#b71c1c

    Start([Start]):::startEnd --> Auth{Auth Successful}:::decision
    Auth -->|No| AuthFail[Display Error Banner]:::error
    AuthFail --> End1([End]):::startEnd
    Auth -->|Yes| Dashboard[Open Clinical Dashboard]:::process

    Dashboard --> SelectAction{User Action}:::decision

    SelectAction -->|Upload Image| Upload[Upload DICOM File]:::process
    Upload --> ValidDICOM{Valid DICOM Format}:::decision
    ValidDICOM -->|No| UploadError[Show Error Toast]:::error
    UploadError --> SelectAction
    ValidDICOM -->|Yes| ParseHeader[Extract Metadata Headers]:::process
    ParseHeader --> Normalize[Normalize Pixel Array]:::process
    Normalize --> SaveDB[(Save Metadata to SQLite DB)]:::database
    SaveDB --> RenderThumb[Render PNG Thumbnail in Canvas]:::process
    RenderThumb --> SelectAction

    SelectAction -->|Analyze Image| Analyze[Trigger CNN Inference Engine]:::process
    Analyze --> ComputeScores[Compute Softmax Confidence Scores]:::process
    ComputeScores --> ComputeBoxes[Calculate Spatial Bounding Boxes]:::process
    ComputeBoxes --> SaveResults[(Save Prediction Results to DB)]:::database
    SaveResults --> DrawCanvas[Draw Bounding Box Overlays on Canvas]:::process
    DrawCanvas --> ShowResults[Display Category Label and Confidence]:::process
    ShowResults --> DoctorReview{Doctor Reviewing}:::decision

    DoctorReview -->|Edit Notes| EditNotes[Edit Clinical Annotation Notes]:::process
    EditNotes --> SaveNotes[(Save Notes to DB)]:::database
    SaveNotes --> DoctorReview

    DoctorReview -->|Generate Draft| DraftPDF[Assemble PDF Template Draft]:::process
    DraftPDF --> ReviewPDF{Doctor Approves Draft}:::decision
    ReviewPDF -->|No| EditNotes
    ReviewPDF -->|Yes| SignOff[Sign Off and Finalize Report]:::process
    SignOff --> CompilePDF[Compile Locked PDF Document]:::process
    CompilePDF --> LockRecord[(Lock Case Record in DB)]:::database
    LockRecord --> NotifyUser[Notify Report Ready for Download]:::process
    NotifyUser --> End2([End - Case Closed]):::startEnd

    SelectAction -->|Logout| Logout[Invalidate JWT Session Token]:::process
    Logout --> End3([End - Session Ended]):::startEnd
```

---

## Legend

| Color | Node Type | Examples |
| :--- | :--- | :--- |
| 🔵 Blue (filled) | Start / End terminals | Start, End |
| 🔵 Blue (outline) | Process steps | Upload, Normalize, CompilePDF |
| 🟡 Amber | Decision points | Auth Check, Valid DICOM, Doctor Review |
| 🟢 Green | Database operations | Save Metadata, Save Results, Lock Record |
| 🔴 Red | Error states | Display Error Banner, Show Error Toast |

---

## Swimlane Summary

| Phase | Actor | Key Activities |
| :--- | :--- | :--- |
| **Authentication** | Any Role | Login, JWT issuance, session management |
| **Image Upload** | Radiologist | DICOM validation, metadata extraction, thumbnail rendering |
| **AI Analysis** | System (Automated) | CNN inference, softmax scoring, bounding box generation |
| **Review and Annotation** | Doctor | Clinical notes entry, draft PDF generation, sign-off |
| **Report Finalization** | System | PDF compilation, DB lock, notification |

---

> [!NOTE]
> This diagram is rendered via Mermaid.js. For print/export, save as `activity_preprocess_workflow.png`.
