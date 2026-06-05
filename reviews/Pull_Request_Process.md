# Pull Request (PR) & Code Integration Guide

This guide establishes the branch structure, commit formatting protocols, and Pull Request (PR) submission workflows enforced to maintain documentation and code quality in the repository.

---

## 1. Branch Naming Conventions

Every modification or new section must be authored on a dedicated feature branch. Direct commits to `develop` or `main` are restricted.

- **Documentation Branches:** `doc/{phase}-{subject}`
  - *Examples:* `doc/doc1-srs-draft`, `doc/doc2-uml-diagrams`, `doc/doc3-installation-manual`
- **Quality Assurance & Review Branches:** `review/{document-type}`
  - *Examples:* `review/srs-audit-checklist`, `review/user-guides-validation`
- **Infrastructure & Settings Branches:** `infra/{setting-name}`
  - *Examples:* `infra/github-pr-template`, `infra/update-gitignore`

---

## 2. Commit Format Guide

All commit messages must comply with the prefix rules defined in [Documentation_Standards.md](../docs/Documentation_Standards.md):

`[PREFIX]: [Action description]`

- **`DOC1:`** Software Requirements Specification (SRS) tasks.
- **`DOC2:`** Software Design Document (SDD) and diagram tasks.
- **`DOC3:`** User Manuals, Installation Guides, and Test Documentation.
- **`REPORT:`** Final Project Report tasks.
- **`INFRA:`** Repository infrastructure, `.gitignore`, directory layouts, and standards documentation.

*Example Commit:* `DOC1: Updated functional requirement FR-03 with coordinate outputs`

---

## 3. Pull Request Submission Lifecycle

To merge progress into the active `develop` branch, authors must complete the following steps:

```text
+-----------------------+
|  1. Push Branch       |  - Push local feature branch to GitHub remote.
+-----------+-----------+
            |
            v
+-----------------------+
|  2. Open Pull Request |  - Target develop as the base integration branch.
|                       |  - PR template auto-populates in GitHub interface.
+-----------+-----------+
            |
            v
+-----------------------+
|  3. Fill PR Template  |  - Complete description, affected files, and checklists.
+-----------+-----------+
            |
            v
+-----------------------+
|  4. Assign Reviewer   |  - Assign peer developers or supervisor for checks.
+-----------+-----------+
            |
            v
+-----------------------+
|  5. Review & Sign-off |  - Reviewer inspects code using QA checklists.
|                       |  - Commits approved changes.
+-----------+-----------+
            |
            v
+-----------------------+
|  6. Merge PR          |  - Merged into develop.
|                       |  - Delete feature branch from remote.
+-----------------------+
```
