# System Architecture Diagram
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** Architecture Overview  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## 4-Tier System Architecture

```mermaid
graph TB
    classDef tier1 fill:#e3f2fd,stroke:#1a73e8,color:#0d47a1
    classDef tier2 fill:#e8f5e9,stroke:#2e7d32,color:#1b5e20
    classDef tier3 fill:#fff8e1,stroke:#f9a825,color:#4a3000
    classDef tier4 fill:#fce4ec,stroke:#c62828,color:#b71c1c
    classDef api fill:#1a73e8,stroke:#0d47a1,color:#ffffff

    subgraph "Tier 1 - Presentation Layer"
        UI_Login["Login Screen"]:::tier1
        UI_Upload["DICOM Upload Panel"]:::tier1
        UI_Canvas["Clinical Canvas Viewer"]:::tier1
        UI_Dashboard["Results Dashboard"]:::tier1
    end

    subgraph "Tier 2 - Business Logic Layer"
        Auth["Auth Controller"]:::tier2
        Router["API Router"]:::tier2
        DICOM_Handler["DICOM Handler"]:::tier2
        Report_Compiler["Report Compiler"]:::tier2
    end

    subgraph "Tier 3 - AI Detection Layer"
        Model_Loader["Model Loader"]:::tier3
        Inference["CNN Inference Engine"]:::tier3
        Spatial["Spatial Bounding Box Analyzer"]:::tier3
    end

    subgraph "Tier 4 - Database Layer"
        DB_Users["users table"]:::tier4
        DB_Images["images table"]:::tier4
        DB_Results["results table"]:::tier4
        DB_Reports["reports table"]:::tier4
        FileStore["DICOM File Cache"]:::tier4
    end

    UI_Login -->|"POST /api/auth/login"| Auth
    UI_Upload -->|"POST /api/images/upload"| Router
    UI_Canvas -->|"GET /api/predictions/id"| Router
    UI_Dashboard -->|"POST /api/reports/export"| Router

    Auth --> Router
    Router --> DICOM_Handler
    Router --> Report_Compiler
    DICOM_Handler -->|"NumPy tensors"| Inference
    Model_Loader --> Inference
    Inference --> Spatial
    Spatial -->|"scores and boxes"| Router

    Router --> DB_Users
    DICOM_Handler --> DB_Images
    DICOM_Handler --> FileStore
    Inference --> DB_Results
    Report_Compiler --> DB_Reports
```

---

## Layer Color Legend

| Color | Tier | Technology |
| :--- | :--- | :--- |
| 🔵 Blue | Presentation Layer | HTML5, CSS3, Vanilla JS |
| 🟢 Green | Business Logic Layer | Python, FastAPI / Flask |
| 🟡 Amber | AI Detection Layer | PyTorch, CUDA, NumPy |
| 🔴 Red | Database Layer | SQLite, Local Filesystem |

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
> This diagram is rendered via Mermaid.js. For print/export, save as `architecture_system_layers.png`.
