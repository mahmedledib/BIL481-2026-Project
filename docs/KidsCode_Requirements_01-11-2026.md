# KidsCode (Kids Code Academy)

## Requirements Document

Course: BIL 481 – Software Engineering  
Assignment: Project Assignment 1  
Contributing authors: Arjen Tüysüz and Mohamed Ahmed Ledib  
Finalization date: November 1, 2026  
Requirements baseline: Kids Code Academy – Requirements v0.14

## Table of Contents

1. Purpose and Priorities
2. Functional Requirements
3. Non-Functional Requirements
4. Verification Strategy
5. Requirements Traceability
6. Document Contribution Matrix

## 1. Purpose and Priorities

This document is an assignment-oriented selection and restatement of Kids Code Academy Requirements v0.14. P0 = foundation; P1 = required before first academy rollout; P2 = post-rollout. IDs below are assignment IDs; the source reference in parentheses identifies the corresponding v0.14 topic or requirement where applicable.

## 2. Functional Requirements

- **FR-01 — Organization isolation (TEN) [P0]** The system shall attach an organization ID to each organization-scoped record and reject requests accessing records outside the authenticated user’s permitted organization.

- **FR-02 — Scoped roles (RBAC) [P0]** The system shall enforce permissions for Platform Admin, Content Author, Translator, Org Admin, Teacher and Parent, allowing multiple scoped roles per account.

- **FR-03 — Secure parent onboarding (AUTH) [P0]** The system shall support one-time parent account setup via a setup link or QR code, allowing the parent to set a password.

- **FR-04 — Curriculum tree (CUR) [P0]** The system shall represent content as Course → Lesson → Level → Stop, where each stop is a puzzle or information stop.

- **FR-05 — Blockly puzzles (PUZ) [P0]** The system shall allow learners to construct and submit solutions with a block-based editor for supported puzzle stops.

- **FR-06 — Python puzzles (PUZ) [P1]** The system shall allow learners to write and submit Python solutions for supported puzzle stops.

- **FR-07 — Evaluation and attempts (EVL) [P0]** The system shall record each completed attempt, including submitted program and result, without overwriting earlier attempts; best score shall be derived from stored attempts.

- **FR-08 — Continue navigation (LRN-01) [P1]** The child home shall provide one Continue action that opens the next unsolved stop in the current course.

- **FR-09 — Course map (LRN) [P1]** The system shall display course progress on a course map and indicate completed and available stops.

- **FR-10 — Class management (MGT-06) [P0]** Authorized organization admins shall create classes, assign teachers, bind course and content language, and manage membership.

- **FR-11 — Authoring (AUT) [P1]** Authorized authors shall create/edit content through draft and preview workflows without editing internal immutable IDs.

- **FR-12 — Publishing (AUT) [P1]** The system shall publish versioned content after required validation; published content shall not be changed by editing an unpublished draft.

- **FR-13 — Language preferences (LOC-01/02) [P0]** The system shall configure interface language per user/child and course content language per class independently.

- **FR-14 — Language switching (LOC-07/08) [P0]** Switching interface language shall preserve progress and workspace code while updating translations and RTL/LTR layout.

- **FR-15 — Dashboards (LRN/MGT) [P1]** Authorized parents and teachers shall view progress only for children within their permitted relationships or classes.

- **FR-16 — Classroom sign-in [P2]** The system shall support class-code and picture-password sign-in for shared classroom devices after initial rollout.

## 3. Non-Functional Requirements

- **NFR-01 — PERF-01 [P1]** First puzzle visit transfers at most 500 KB and makes at most 20 requests, excluding Python runtime.

- **NFR-02 — PERF-05 [P1]** p95 server response time ≤300 ms for child-facing requests and ≤1 s for admin pages.

- **NFR-03 — SEC-03 / sessions [P0]** Use opaque server-side hashed session tokens, delivered in HttpOnly cookies rather than browser storage.

- **NFR-04 — TEN / isolation [P0]** Every protected API endpoint shall pass tests demonstrating organization isolation.

- **NFR-05 — ARC-01/02 [P0]** API shall be stateless; static assets served via CDN; no child-facing request shall call a third-party API.

- **NFR-06 — PERF-03 [P1]** Blockly shall load only for puzzle stops; Python runtime shall load only in Python mode.

- **NFR-07 — LOC-08/09 [P0]** RTL/LTR layout and bidirectional isolation shall work correctly, including code and identifiers.

- **NFR-08 — SEC-04 [P0]** Collect only necessary child data (such as display name, class and progress), not unnecessary identifying data.

- **NFR-09 — PERF-02 [P0]** Content-hashed assets shall be cached as immutable; entry page shall be revalidated.

## 4. Verification Strategy

Use unit tests for curriculum validation and scoring; integration tests for session, data storage and role checks; end-to-end tests for learner and author flows; endpoint-level tenant isolation tests; browser network audits for transfer/request budgets; load tests for p95 response targets; and Arabic/French RTL/LTR visual and functional checks. Define workload and device profiles before recording final performance results.

## 5. Requirements Traceability

| Area | Assignment IDs | Planned evidence |
|---|---|---|
| Security and tenancy | FR-01–03, NFR-03–05 | Access-control and isolation test logs |
| Learning and evaluation | FR-04–09 | Puzzle acceptance tests, attempt records |
| Management and content | FR-10–12, FR-15 | Admin/author E2E test reports |
| Localization | FR-13–14, NFR-07 | Language-switching and layout tests |
| Performance | NFR-01–02, NFR-06, NFR-09 | Network and latency measurements |
| Future scope | FR-16 | Deferred P2 backlog item |

## 6. Document Contribution Matrix

| Document task | Responsible (reviewer) |
|---|---|
| Introduction and prioritization | Arjen Tüysüz (reviewer: Mohamed Ahmed Ledib) |
| Functional requirements | Arjen Tüysüz (reviewer: Mohamed Ahmed Ledib) |
| Non-functional requirements | Mohamed Ahmed Ledib (reviewer: Arjen Tüysüz) |
| Verification and traceability | Arjen Tüysüz (reviewer: Mohamed Ahmed Ledib) |
| Final review and formatting | Mohamed Ahmed Ledib (reviewer: Arjen Tüysüz) |

Each section had one responsible author and one reviewer; GitHub history shows individual edits and reviews.
