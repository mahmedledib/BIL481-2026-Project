# KidsCode (Kids Code Academy)

## Project Plan Document

Course: BIL 481 – Software Engineering  
Assignment: Project Assignment 1  
Contributing authors: Arjen Tüysüz and Mohamed Ahmed Ledib  
Finalization date: November 1, 2026  
Requirements baseline: Kids Code Academy – Requirements v0.14

## Table of Contents

1. Scope and Objectives
2. Organization and Roles
3. Method and Timeline
4. Resources and Budget
5. Effort Estimates
6. Functional Task Allocation
7. Risk Management
8. Communication Plan
9. Change Management
10. Closure and Evaluation
11. Document Contribution Matrix

## 1. Scope and Objectives

Implement the selected P0 and P1 requirements of Kids Code Academy v0.14: organization isolation, secure roles, curriculum, Blockly/Python puzzles, attempt history, learning navigation, content management, multilingual UI and deployment. P2 classroom sign-in and offline shell are outside the initial commitment. Execution and management objectives: (1) pass each phase gate in Section 3 on its planned date; (2) keep actual effort within the 300-hour estimate and report any deviation at closure; (3) merge every change through a reviewed pull request; (4) complete P0 before P1 and keep P2 out of the initial commitment.

## 2. Organization and Roles

Mohamed Ahmed Ledib: project manager (final decisions), system architect (infrastructure and system design), designer (UI and data model), developer.

Arjen Tüysüz: requirements analyst, lead developer, tester (QA).

Each task has one owner and one reviewer (Sections 5 and 6). Design decisions and code changes are reviewed through pull requests; work is assigned and recorded through GitHub Issues, branches and commits.

## 3. Method and Timeline

Use short Agile-inspired iterations with weekly reviews, GitHub Issues for tasks, pull requests for review, and automated checks before integration.

| Phase | Dates | Deliverable |
|---|---|---|
| Requirements | 02–08 Nov 2026 | Accepted baseline and tests |
| Architecture and design | 09–22 Nov 2026 | Architecture, data model and UI design |
| Foundation | 23 Nov–13 Dec 2026 | Roles, isolation, curriculum, localization |
| Core features | 14 Dec 2026–10 Jan 2027 | Puzzles, grading, dashboards, authoring |
| Integration/testing | 11–24 Jan 2027 | System and performance test reports |
| Deployment/evaluation | 25–31 Jan 2027 | Deployed prototype, closure report |

Key dates: Assignment-1 documents: 01 Nov 2026; design gate: 22 Nov; foundation gate: 13 Dec; integrated prototype: 10 Jan; test gate: 24 Jan; final evaluation and closure: 31 Jan 2027.

## 4. Resources and Budget

Two existing laptops, Git/GitHub, TypeScript, Blockly, Pyodide, browsers, Cloudflare Workers/D1 and object storage/CDN. Planned effort is 300 person-hours; 150 per team member. No new hardware is budgeted. Any paid cloud usage requires team review and approval; a precise monetary estimate cannot be established without expected traffic and hosting quotas.

## 5. Effort Estimates

Estimation method: bottom-up task decomposition with team judgment. Hours represent planned work, not logged actual effort. Each task has one owner, who carries most of its hours, and one reviewer.

| Task | Arjen h | Mohamed h | Total h |
|---|---|---|---|
| Requirements analysis and documentation (owner: Arjen) | 16 | 8 | 24 |
| Architecture and UI/database design (owner: Mohamed) | 12 | 28 | 40 |
| Authentication and organization foundation (owner: Mohamed) | 12 | 24 | 36 |
| Curriculum and localization foundation (owner: Mohamed) | 14 | 22 | 36 |
| Blockly and Python interfaces (owner: Arjen) | 32 | 20 | 52 |
| Evaluation, progress, dashboards and authoring (owner: Arjen) | 30 | 22 | 52 |
| Integration and testing (owner: Arjen) | 30 | 14 | 44 |
| Deployment and evaluation (owner: Mohamed) | 4 | 12 | 16 |
| TOTAL | 150 | 150 | 300 |

Phase totals: requirements 24 h; design 40 h; foundation 72 h; core features 104 h; testing 44 h; deployment 16 h. Total = 300 person-hours: 150 per member (about 11.5 hours per person per week over the 13 weeks from 2 Nov 2026 to 31 Jan 2027).

## 6. Functional Task Allocation

| Workstream / requirement IDs | Arjen | Mohamed |
|---|---|---|
| Auth, roles, tenancy — FR-01–03 | Reviewer | Owner |
| Curriculum — FR-04 | Reviewer | Owner |
| Blockly and Python puzzles — FR-05–06 | Owner | Reviewer |
| Evaluation and learner flow — FR-07–09 | Owner | Reviewer |
| Classes and content — FR-10–12 | Owner | Reviewer |
| Localization — FR-13–14 | Reviewer | Owner |
| Dashboards — FR-15 | Owner | Reviewer |
| Performance, security, deployment — NFR-01–09 | Reviewer | Owner |
| P2 class sign-in — FR-16 | Deferred | Deferred |

Rationale: Tasks follow the roles each member chose and the team agreed. Mohamed, a mathematician learning engineering, owns architecture and design work to build decision-making and system-design skills; Arjen owns requirements, development and testing work to build implementation and QA skills. Each owner carries most of the task hours and the other member reviews, so both plan 150 hours and every area is known by two people.

## 7. Risk Management

| Risk | Likelihood / impact | Response |
|---|---|---|
| Tenant data leak | Medium / High | Centralized checks, per-endpoint isolation tests |
| Unsafe puzzle content | Medium / High | Sandboxing, content validation, CI-tested game code |
| Pyodide or low-end device performance | Medium / High | Early spike, lazy loading, network budget tests |
| RTL/LTR bugs | Medium / Medium | Arabic/French test matrix and regression tests |
| Schedule pressure | High / High | P0 first; defer P2; weekly re-estimation |
| Member absence / knowledge silo | Medium / Medium | Pair reviews, shared notes and cross-component work |

## 8. Communication Plan

Weekly synchronous review to assess completed work, blockers, risks and upcoming tasks; asynchronous messaging as needed; GitHub Issues for decisions and task status; pull requests for peer review; milestone demonstrations for stakeholder feedback. Record action items and owners in the repository.

## 9. Change Management

Every change is logged as an issue, mapped to v0.14 IDs, assessed for scope/effort/risk/test impact, reviewed by both members and approved by the project manager for baseline changes, scheduled by P0/P1/P2 priority, and reflected in requirements, tests and the plan. P2 changes do not displace unfinished P0/P1 work without explicit approval.

## 10. Closure and Evaluation

At the planned closure on 31 Jan 2027, compare delivered P0/P1 requirements against acceptance tests, verify organization isolation, measure first-visit network budgets and p95 latency, inspect deployment logs, document remaining issues, and archive final deliverables. Actual effort and deviations from the 300-hour estimate will be reported.

## 11. Document Contribution Matrix

| Document task | Responsible (reviewer) |
|---|---|
| Scope, objectives and team organization | Mohamed Ahmed Ledib (reviewer: Arjen Tüysüz) |
| Methodology and timeline | Mohamed Ahmed Ledib (reviewer: Arjen Tüysüz) |
| Resources, budget and effort estimates | Arjen Tüysüz (reviewer: Mohamed Ahmed Ledib) |
| Requirement-to-task allocation | Arjen Tüysüz (reviewer: Mohamed Ahmed Ledib) |
| Risks, communication and change management | Mohamed Ahmed Ledib (reviewer: Arjen Tüysüz) |
| Closure criteria and final review | Arjen Tüysüz (reviewer: Mohamed Ahmed Ledib) |

Each section had one responsible author and one reviewer; commit history and revision records show individual contributions.
