# System Architecture Diagram
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** Architecture Overview  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## 4-Tier System Architecture

```mermaid
graph TB
    subgraph "Tier 1: Presentation Layer (Web Browser)"
        UI_Login["🔐 Login Screen"]
        UI_Upload["📂 DICOM Upload Panel"]
        UI_Canvas["🖼️ Clinical Canvas Viewer"]
        UI_Dashboard["📊 Results Dashboard"]
    end

    subgraph "Tier 2: Business Logic Layer (Python Web API)"
        Auth["Auth Controller\n(JWT / PBKDF2)"]
        Router["API Router\n(FastAPI / Flask)"]
        DICOM_Handler["DICOM Handler\n(pydicom parser)"]
        Report_Compiler["Report Compiler\n(ReportLab PDF)"]
    end

    subgraph "Tier 3: AI Detection Layer (CUDA GPU)"
        Model_Loader["Model Loader\n(Pre-trained Weights)"]
        Inference["CNN Inference Engine\n(PyTorch / TensorFlow)"]
        Spatial["Spatial Analyzer\n(Bounding Box Detection)"]
    end

    subgraph "Tier 4: Database Layer (SQLite)"
        DB_Users["users table"]
        DB_Images["images table"]
        DB_Results["results table"]
        DB_Reports["reports table"]
        FileStore["📁 DICOM File Cache\n(Local Filesystem)"]
    end

    UI_Login -->|"HTTPS POST /api/auth/login"| Auth
    UI_Upload -->|"HTTPS POST /api/images/upload"| Router
    UI_Canvas -->|"HTTPS GET /api/predictions/{id}"| Router
    UI_Dashboard -->|"HTTPS POST /api/reports/export"| Router

    Auth --> Router
    Router --> DICOM_Handler
    Router --> Report_Compiler
    DICOM_Handler -->|"NumPy tensors"| Inference
    Model_Loader --> Inference
    Inference --> Spatial
    Spatial -->|"scores & boxes"| Router

    Router -->|"SQL queries"| DB_Users
    DICOM_Handler -->|"SQL + file write"| DB_Images
    DICOM_Handler --> FileStore
    Inference -->|"SQL write"| DB_Results
    Report_Compiler -->|"SQL write"| DB_Reports
```

---

## Component Communication Summary

| Source | Destination | Protocol / Method |
| :--- | :--- | :--- |
| Web Browser | Backend API | HTTPS / RESTful JSON |
| Backend API | AI Engine | Internal Python memory (NumPy arrays) |
| Backend API | SQLite DB | SQL queries via SQLite3 |
| AI Engine | GPU Memory | CUDA kernel operations |
| DICOM Handler | Local Storage | OS filesystem read/write |

---

> [!NOTE]
> This diagram is rendered via Mermaid.js in markdown viewers (GitHub, GitLab, VS Code with Mermaid extension).
> The equivalent PNG export should be saved as `architecture_system_layers.png` in this directory for PDF inclusions.
