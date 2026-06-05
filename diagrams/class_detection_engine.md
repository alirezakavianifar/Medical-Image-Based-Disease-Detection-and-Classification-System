# Class Diagram – System Object Model
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** UML Class Diagram  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## Class Diagram

```mermaid
classDiagram
    direction TB

    class User {
        +int userID
        +String name
        +String email
        +String passwordHash
        +String role
        +DateTime createdAt
        +login(email: String, password: String) bool
        +logout() bool
        +getRole() String
    }

    class MedicalImage {
        +int imageID
        +String patientID
        +String patientName
        +Date patientDOB
        +String modality
        +DateTime uploadDate
        +String rawFilePath
        +String pngFilePath
        +parseHeader(filePath: String) Metadata
        +saveMetadata(meta: Metadata) bool
        +preprocess() Array
        +renderThumbnail() String
    }

    class DetectionEngine {
        +int engineID
        +String modelWeightPath
        +String deviceType
        +loadWeights() bool
        +computeBoundingBoxes(tensor: Array) Array
        +releaseGPUMemory() void
    }

    class ClassificationEngine {
        +int engineID
        +String modelWeightPath
        +String[] classLabels
        +loadWeights() bool
        +forwardPass(tensor: Array) Array
        +computeSoftmax(logits: Array) Array
        +getPredictedLabel(scores: Array) String
    }

    class DiagnosticResult {
        +int resultID
        +int imageID
        +String diseaseType
        +float confidenceScore
        +Array boundingBoxCoordinates
        +DateTime analyzedAt
        +saveToDatabase() bool
        +toJSON() String
    }

    class Report {
        +int reportID
        +int imageID
        +int doctorID
        +String clinicalComments
        +bool isFinalized
        +String pdfFilePath
        +DateTime finalizedAt
        +assembleTemplate() String
        +compilePDF() bytes
        +lockReport() bool
        +exportDownloadURL() String
    }

    class AuthController {
        +verifyCredentials(email: String, password: String) bool
        +issueJWT(userID: int, role: String) String
        +validateJWT(token: String) Payload
        +enforceRole(token: String, requiredRole: String) bool
    }

    %% Relationships
    User "1" --> "many" MedicalImage : uploads
    User "1" --> "many" Report : signs_off
    MedicalImage "1" --> "1" DiagnosticResult : generates
    MedicalImage "1" --> "1" Report : documented_in
    DetectionEngine ..> MedicalImage : processes
    ClassificationEngine ..> MedicalImage : classifies
    ClassificationEngine --> DiagnosticResult : produces
    DetectionEngine --> DiagnosticResult : produces
    AuthController ..> User : authenticates
```

---

## Key Method Descriptions

| Class | Method | Responsibility |
| :--- | :--- | :--- |
| `User` | `login()` | Verifies credentials and initiates session |
| `MedicalImage` | `preprocess()` | Returns normalized NumPy tensor from DICOM pixel data |
| `DetectionEngine` | `computeBoundingBoxes()` | Returns `[[xmin, ymin, xmax, ymax], ...]` array |
| `ClassificationEngine` | `computeSoftmax()` | Converts raw logits to confidence probability array |
| `Report` | `compilePDF()` | Returns binary PDF bytes from assembled template |
| `AuthController` | `enforceRole()` | Blocks non-authorized roles from clinical endpoints |

---

> [!NOTE]
> This diagram is rendered via Mermaid.js. For print/export, save as `class_detection_engine.png`.
