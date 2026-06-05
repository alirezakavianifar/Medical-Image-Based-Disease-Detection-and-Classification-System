# Project Gantt Chart
## Medical Image-Based Disease Detection and Classification System

**Diagram Type:** Project Timeline / Gantt Chart  
**Version:** v1.0.0  
**Date:** June 5, 2026  

---

## 8-Week Project Gantt Chart

```mermaid
gantt
    title Medical Image Disease Detection – Documentation Project Timeline
    dateFormat  YYYY-MM-DD
    axisFormat  %b %d

    section Phase 1: Project Initialization
    Project Charter & Scope Definition     :done, p1a, 2026-04-01, 3d
    Git Repository Setup & Configuration   :done, p1b, after p1a, 2d
    Documentation Standards Definition     :done, p1c, after p1b, 2d

    section Phase 2: Requirements (SRS)
    Stakeholder Interviews & Review        :done, p2a, 2026-04-08, 3d
    SRS Drafting – Sections 1 & 2         :done, p2b, after p2a, 2d
    SRS Drafting – Functional Requirements :done, p2c, after p2b, 2d
    SRS Drafting – Non-Functional & Interfaces :done, p2d, after p2c, 2d
    SRS Peer Review & Approval            :done, p2e, after p2d, 2d
    Git Tag: v1.0-SRS                     :milestone, m1, after p2e, 0d

    section Phase 3: System Design (SDD)
    UML Use Case & Activity Diagrams       :done, p3a, 2026-04-22, 3d
    Class Diagram & Sequence Diagram       :done, p3b, after p3a, 2d
    4-Tier Architecture Definition         :done, p3c, after p3b, 2d
    Database ERD & Schema Specification    :done, p3d, after p3c, 2d
    API Endpoint Contracts                 :done, p3e, after p3d, 2d
    SDD Peer Review & Approval             :done, p3f, after p3e, 2d
    Git Tag: v1.0-SDD                      :milestone, m2, after p3f, 0d

    section Phase 4: User & Test Documentation
    User Manual Drafting                   :done, p4a, 2026-05-13, 3d
    Installation & Deployment Guide        :done, p4b, after p4a, 2d
    Test Case Specifications & Execution   :done, p4c, after p4b, 3d
    API Reference (OpenAPI / Swagger)      :done, p4d, after p4c, 2d
    User Validation Role-Play              :done, p4e, after p4d, 2d
    Git Tag: v1.0-DOC3                     :milestone, m3, after p4e, 0d

    section Phase 5: Quality Assurance
    Documentation QA Plan & RTM           :done, p5a, 2026-05-27, 2d
    Pull Request Process Guide             :done, p5b, after p5a, 2d
    GitHub PR Template Implementation      :done, p5c, after p5b, 1d

    section Phase 6: Final Report & Release
    Final Report Drafting                  :done, p6a, 2026-06-03, 2d
    Final Report Peer Review               :done, p6b, after p6a, 1d
    Repository Archival & Release Tag      :done, p6c, after p6b, 1d
    Git Tag: v1.0-FINAL                    :milestone, m4, after p6c, 0d
```

---

## Milestone Summary

| Milestone | Tag | Target Date | Status |
| :--- | :--- | :--- | :---: |
| Requirements Baseline | `v1.0-SRS` | Week 3 End | ✅ PASSED |
| System Design Baseline | `v1.0-SDD` | Week 5 End | ✅ PASSED |
| Documentation Suite Baseline | `v1.0-DOC3` | Week 7 End | ✅ PASSED |
| Final Project Release | `v1.0-FINAL` | Week 8 End | ✅ PASSED |

---

> [!NOTE]
> This Gantt chart is rendered via Mermaid.js. For print/export, save as `gantt_project_timeline.png`.
