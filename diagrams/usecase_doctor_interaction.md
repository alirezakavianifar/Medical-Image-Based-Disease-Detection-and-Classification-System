# UML Use Case Diagram
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** Use Case  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## Use Case Diagram

```mermaid
graph TD
    Admin(["Administrator"])
    Doctor(["Doctor"])
    Radiologist(["Radiologist"])

    subgraph "Medical Image Classification System"
        UC1("UC-01: Authenticate and Login")
        UC2("UC-02: Upload DICOM Image")
        UC3("UC-03: Run AI Inference")
        UC4("UC-04: View Scan and Annotations")
        UC5("UC-05: Edit Clinical Notes")
        UC6("UC-06: Sign Off and Export PDF Report")
        UC7("UC-07: Manage User Accounts")
        UC8("UC-08: View Audit Logs")
    end

    Admin --- UC1
    Admin --- UC7
    Admin --- UC8

    Doctor --- UC1
    Doctor --- UC4
    Doctor --- UC5
    Doctor --- UC6

    Radiologist --- UC1
    Radiologist --- UC2
    Radiologist --- UC3
    Radiologist --- UC4
    Radiologist --- UC5
```

---

## Use Case Descriptions

| Use Case ID | Title | Primary Actor | Precondition | Postcondition |
| :--- | :--- | :--- | :--- | :--- |
| **UC-01** | Authenticate and Login | All Roles | System is running | JWT session token issued |
| **UC-02** | Upload DICOM Image | Radiologist | Logged-in session | Image stored, metadata parsed |
| **UC-03** | Run AI Inference | Radiologist | Image uploaded | Bounding boxes and confidence scores returned |
| **UC-04** | View Scan and Annotations | Doctor, Radiologist | Inference completed | Canvas with overlays displayed |
| **UC-05** | Edit Clinical Notes | Doctor, Radiologist | Case open in dashboard | Notes saved to DB |
| **UC-06** | Sign Off and Export PDF | Doctor | Notes added | PDF compiled and case locked |
| **UC-07** | Manage User Accounts | Administrator | Admin session active | User records updated |
| **UC-08** | View Audit Logs | Administrator | Admin session active | Audit log report viewed |

---

> [!NOTE]
> This diagram is rendered via Mermaid.js. For print/export, save as `usecase_doctor_interaction.png`.
