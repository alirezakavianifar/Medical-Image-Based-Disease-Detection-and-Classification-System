# Entity Relationship Diagram (ERD) – Database Schema
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** Entity Relationship (ERD)  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## Database ERD

```mermaid
erDiagram
    USERS {
        int user_id PK "AUTOINCREMENT"
        string name "NOT NULL"
        string email UK "UNIQUE, NOT NULL"
        string password_hash "NOT NULL"
        string role "Admin | Doctor | Radiologist"
        datetime created_at "DEFAULT CURRENT_TIMESTAMP"
    }

    IMAGES {
        int image_id PK "AUTOINCREMENT"
        string patient_id "NOT NULL"
        string patient_name "NULLABLE"
        date patient_dob "NULLABLE"
        string modality "CT | MR | CR"
        datetime upload_date "NOT NULL"
        int uploaded_by_id FK "REFERENCES users"
        string raw_file_path "NOT NULL"
        string png_file_path "NOT NULL"
    }

    RESULTS {
        int result_id PK "AUTOINCREMENT"
        int image_id FK "UNIQUE, REFERENCES images"
        string disease_type "NOT NULL"
        real confidence_score "0.0 to 1.0"
        text bounding_box_coordinates "JSON Array"
        datetime analyzed_at "DEFAULT CURRENT_TIMESTAMP"
    }

    REPORTS {
        int report_id PK "AUTOINCREMENT"
        int image_id FK "UNIQUE, REFERENCES images"
        int doctor_id FK "REFERENCES users"
        text clinical_comments "NULLABLE"
        boolean is_finalized "DEFAULT FALSE"
        string pdf_file_path "NULLABLE"
        datetime finalized_at "NULLABLE"
    }

    USERS ||--o{ IMAGES : "uploads"
    USERS ||--o{ REPORTS : "signs off"
    IMAGES ||--|| RESULTS : "has one"
    IMAGES ||--|| REPORTS : "documented in"
```

---

## Table Index Summary

| Index Name | Table | Column(s) | Purpose |
| :--- | :--- | :--- | :--- |
| `idx_users_email` | `users` | `email` | Fast login authentication queries |
| `idx_images_patient_id` | `images` | `patient_id` | Quick patient case history lookup |
| `idx_images_uploaded_by_id` | `images` | `uploaded_by_id` | Filter scans by uploading clinician |
| `idx_results_image_id` | `results` | `image_id` | Fast AI result display on dashboard |
| `idx_reports_image_id` | `reports` | `image_id` | Quick report sign-off status check |

---

> [!NOTE]
> This ERD is rendered via Mermaid.js. For print/export, save as `database_schema_erd.png`.
