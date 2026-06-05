# Activity Diagram – Image Processing Workflow
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** Activity / Workflow  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## End-to-End Clinical Workflow

```mermaid
flowchart TD
    Start([🚀 Start: User Logs In]) --> Auth{Authentication\nSuccessful?}
    Auth -->|No| AuthFail[Display Error Banner\nInvalid Credentials] --> End1([End])
    Auth -->|Yes| Dashboard[Open Clinical Dashboard]

    Dashboard --> SelectAction{User Action}

    SelectAction -->|Upload Image| Upload[Upload DICOM File\nvia Drag-and-Drop]
    Upload --> ValidDICOM{Valid DICOM\nFile Format?}
    ValidDICOM -->|No| UploadError[Show Error Toast:\nInvalid or Oversized File] --> SelectAction
    ValidDICOM -->|Yes| ParseHeader[Extract Metadata Headers\nPatient ID, Modality, Date]
    ParseHeader --> Normalize[Normalize Pixel Array\nResize & Float Conversion]
    Normalize --> SaveDB[(Save Metadata\nto SQLite DB)]
    SaveDB --> RenderThumb[Render Preprocessed\nPNG Thumbnail in Canvas]
    RenderThumb --> SelectAction

    SelectAction -->|Analyze Image| Analyze[Trigger CNN\nInference Engine]
    Analyze --> ComputeScores[Compute Softmax\nConfidence Scores]
    ComputeScores --> ComputeBoxes[Calculate Spatial\nBounding Boxes]
    ComputeBoxes --> SaveResults[(Save Prediction\nResults to DB)]
    SaveResults --> DrawCanvas[Draw Bounding Box\nOverlays on Canvas]
    DrawCanvas --> ShowResults[Display Category Label\n& Confidence %]
    ShowResults --> DoctorReview{Doctor\nReviewing?}

    DoctorReview -->|Edit Notes| EditNotes[Edit Clinical\nAnnotation Notes]
    EditNotes --> SaveNotes[(Save Notes\nto DB)] --> DoctorReview

    DoctorReview -->|Generate Draft| DraftPDF[Assemble PDF\nTemplate Draft]
    DraftPDF --> ReviewPDF{Doctor Approves\nDraft?}
    ReviewPDF -->|No| EditNotes
    ReviewPDF -->|Yes| SignOff[Sign Off &\nFinalize Report]
    SignOff --> CompilePDF[Compile Locked\nPDF Document]
    CompilePDF --> LockRecord[(Lock Case Record\nMark is_finalized = TRUE)]
    LockRecord --> NotifyUser[Notify: Report Ready\nfor Download]
    NotifyUser --> End2([End: Case Closed])

    SelectAction -->|Logout| Logout[Invalidate JWT\nSession Token] --> End3([End: Session Ended])
```

---

## Swimlane Summary

| Phase | Actor | Key Activities |
| :--- | :--- | :--- |
| **Authentication** | Any Role | Login, JWT issuance, session management |
| **Image Upload** | Radiologist | DICOM validation, metadata extraction, thumbnail rendering |
| **AI Analysis** | System (Automated) | CNN inference, softmax scoring, bounding box generation |
| **Review & Annotation** | Doctor | Clinical notes entry, draft PDF generation, sign-off |
| **Report Finalization** | System | PDF compilation, DB lock, notification |

---

> [!NOTE]
> This diagram is rendered via Mermaid.js. For print/export, save as `activity_preprocess_workflow.png`.
