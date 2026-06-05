# Activity Diagram - Image Processing Workflow
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** Activity / Workflow  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## End-to-End Clinical Workflow

```mermaid
flowchart TD
    Start([Start]) --> Auth{Auth Successful}
    Auth -->|No| AuthFail[Display Error Banner]
    AuthFail --> End1([End])
    Auth -->|Yes| Dashboard[Open Clinical Dashboard]

    Dashboard --> SelectAction{User Action}

    SelectAction -->|Upload Image| Upload[Upload DICOM File]
    Upload --> ValidDICOM{Valid DICOM Format}
    ValidDICOM -->|No| UploadError[Show Error Toast]
    UploadError --> SelectAction
    ValidDICOM -->|Yes| ParseHeader[Extract Metadata Headers]
    ParseHeader --> Normalize[Normalize Pixel Array]
    Normalize --> SaveDB[(Save Metadata to SQLite DB)]
    SaveDB --> RenderThumb[Render PNG Thumbnail in Canvas]
    RenderThumb --> SelectAction

    SelectAction -->|Analyze Image| Analyze[Trigger CNN Inference Engine]
    Analyze --> ComputeScores[Compute Softmax Confidence Scores]
    ComputeScores --> ComputeBoxes[Calculate Spatial Bounding Boxes]
    ComputeBoxes --> SaveResults[(Save Prediction Results to DB)]
    SaveResults --> DrawCanvas[Draw Bounding Box Overlays on Canvas]
    DrawCanvas --> ShowResults[Display Category Label and Confidence]
    ShowResults --> DoctorReview{Doctor Reviewing}

    DoctorReview -->|Edit Notes| EditNotes[Edit Clinical Annotation Notes]
    EditNotes --> SaveNotes[(Save Notes to DB)]
    SaveNotes --> DoctorReview

    DoctorReview -->|Generate Draft| DraftPDF[Assemble PDF Template Draft]
    DraftPDF --> ReviewPDF{Doctor Approves Draft}
    ReviewPDF -->|No| EditNotes
    ReviewPDF -->|Yes| SignOff[Sign Off and Finalize Report]
    SignOff --> CompilePDF[Compile Locked PDF Document]
    CompilePDF --> LockRecord[(Lock Case Record in DB)]
    LockRecord --> NotifyUser[Notify Report Ready for Download]
    NotifyUser --> End2([End - Case Closed])

    SelectAction -->|Logout| Logout[Invalidate JWT Session Token]
    Logout --> End3([End - Session Ended])
```

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
