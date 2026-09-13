# BoardFlow — Switchboard Production System
BoardFlow is a lightweight, modular production-control framework designed to eliminate common manufacturing errors in custom switchboard assembly. It provides structured workflows, controlled revision management, BoM verification, and AI-assisted validation from design through assembly and final testing.

BoardFlow is not a replacement for PLM/MES systems — it is a practical, domain-specific hybrid tailored for electrical switchboard manufacturing.

## Core Problems Addressed
- Mixed drawing revisions
- Incorrect component selection (wrong PSU, wrong CB rating, wrong switches)
- Unverified handovers between designers and assemblers
- Lack of traceability
- No single source of truth
- Rework caused by assumptions and undocumented changes

## System Components

### 1. Digital Traveller
A job-specific digital passport containing:
- Latest drawings
- Latest BoM
- Assembly workflow
- Checklists
- Photos
- Test results
- Sign-offs
- AI validation reports

The traveller follows the job from design → assembly → testing → final QC.

### 2. Controlled BoM Picking (Poka-Yoke)
A scanning workflow that ensures:
- Correct part numbers
- Correct voltage ratings
- Correct CB sizes
- Correct controller/PSU compatibility

Wrong parts cannot be picked.

### 3. Workflow Engine (MES-Lite)
Structured assembly steps with:
- Mandatory checklists
- Photo verification
- Handover sign-offs
- Automatic logging

### 4. Drawing & Revision Control (PLM-Lite)
A single authoritative source for:
- Drawings
- Revisions
- Change notes
- Version locking

### 5. AI Validation Layer
AI extracts data from DWGs and cross-checks:
- CB ratings
- PSU voltages
- Controller requirements
- Cable sizes
- Load management components

AI generates a pre-assembly error report.

### 6. Testing Integration (Future)
Eventually, BoardFlow will generate:
- Automated test forms
- Test sequences
- Pass/fail reports
- Integration with custom test hardware

## Long-Term Vision
BoardFlow becomes a complete production ecosystem:

Design → Validation → BoM picking → Assembly → Testing → QC → Documentation → Delivery

## 🧩 Digital Traveller — Deeper Explanation
This is the heart of the system. Think of it as a web app + API + AI backend.

### What it actually is
- **A web app** — accessible on phones, tablets, or PCs.
- **A backend service** — stores job data, revisions, BoMs, checklists, photos, test results.
- **An AI validation module** — reads DWGs, extracts metadata, compares to BoM, flags mismatches.
- **A workflow engine** — defines assembly steps and enforces checklists.
- **A traceability log** — every action is timestamped and attributed.

### How the components communicate

**Frontend (React/Svelte/Vue)**
Displays traveller pages, checklists, BoM scanner, revision viewer.

**Backend (FastAPI / Node / Django)**
Provides REST API endpoints:
- `/jobs/{id}/traveller`
- `/jobs/{id}/bom`
- `/jobs/{id}/drawings`
- `/jobs/{id}/workflow`
- `/jobs/{id}/validation`

**AI module**
Triggered by:
- New drawing upload
- New BoM upload
- Manual "validate" button

AI produces:
- Structured JSON
- Mismatch reports
- Warnings
- Suggested corrections

**Database**
Stores:
- Job metadata
- Revision history
- BoM items
- Scanned parts
- Workflow progress
- Test results

## 🧪 Testing Tool Integration (Future)
Currently, testing relies on tools like Google Forms.

BoardFlow will eventually:
- Auto-generate test forms
- Auto-populate expected values
- Auto-validate results
- Store test reports in the traveller

This is a later phase, but it is documented now for context.
