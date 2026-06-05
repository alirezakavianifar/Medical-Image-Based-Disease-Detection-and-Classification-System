# UML Use Case Diagram
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** Use Case  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## Use Case Diagram

```mermaid
graph TD
    %% Actors
    Admin(["👤 Administrator"])
    Doctor(["🩺 Doctor"])
    Radiologist(["🔬 Radiologist"])

    %% System boundary
    subgraph "Medical Image Classification System"
        UC1("📋 UC-01: Authenticate & Login")
        UC2("📤 UC-02: Upload DICOM Image")
        UC3("🤖 UC-03: Run AI Inference")
        UC4("🖼️ UC-04: View Scan & Annotations")
        UC5("📝 UC-05: Edit Clinical Notes")
        UC6("✅ UC-06: Sign Off & Export PDF Report")
        UC7("👥 UC-07: Manage User Accounts")
        UC8("📊 UC-08: View Audit Logs")
    end

    %% Admin connections
    Admin --- UC1
    Admin --- UC7
    Admin --- UC8

    %% Doctor connections
    Doctor --- UC1
    Doctor --- UC4
    Doctor --- UC5
    Doctor --- UC6

    %% Radiologist connections
    Radiologist --- UC1
    Radiologist --- UC2
    Radiologist --- UC3
    Radiologist --- UC4
    Radiologist --- UC5

    %% Include / Extend relationships
    UC3 -.->|"<<include>>"| UC2
    UC6 -.->|"<<include>>"| UC5
    UC6 -.->|"<<extend>>"| UC4
```

---

## Use Case Descriptions

| Use Case ID | Title | Primary Actor | Precondition | Postcondition |
| :--- | :--- | :--- | :--- | :--- |
| **UC-01** | Authenticate & Login | All Roles | System is running | JWT session token issued |
| **UC-02** | Upload DICOM Image | Radiologist | Logged-in session | Image stored, metadata parsed |
| **UC-03** | Run AI Inference | Radiologist | Image uploaded | Bounding boxes & confidence scores returned |
| **UC-04** | View Scan & Annotations | Doctor, Radiologist | Inference completed | Canvas with overlays displayed |
| **UC-05** | Edit Clinical Notes | Doctor, Radiologist | Case open in dashboard | Notes saved to DB |
| **UC-06** | Sign Off & Export PDF | Doctor | Notes added | PDF compiled and case locked |
| **UC-07** | Manage User Accounts | Administrator | Admin session active | User records updated |
| **UC-08** | View Audit Logs | Administrator | Admin session active | Audit log report viewed |

---

> [!NOTE]
> This diagram is rendered via Mermaid.js. For print/export, save as `usecase_doctor_interaction.png`.
