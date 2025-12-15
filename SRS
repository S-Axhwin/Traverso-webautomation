# Software Requirements Specification (SRS)

## 1. Introduction

### 1.1 Purpose

This document defines the functional and non-functional requirements for the **User-Defined Web Automation and Data Extraction Platform**. The system enables non-technical users to reliably automate browser-based workflows and extract structured data without writing code.

### 1.2 Scope

The platform allows users to:

* Record real browser interactions via a custom browser extension
* Convert interactions into deterministic, versioned workflows
* Execute workflows at scale using headless browsers
* Extract, normalize, and persist structured data
* Monitor execution through logs, screenshots, and job states

The system explicitly avoids prompt-only or AI-guess-based automation and focuses on reliability, repeatability, and observability.

### 1.3 Definitions, Acronyms, and Abbreviations

* **Workflow**: A deterministic sequence of recorded browser actions
* **Job**: A single execution instance of a workflow
* **Worker**: An execution node that runs jobs using Playwright
* **Selector**: DOM path used to locate elements
* **Headless Browser**: Browser running without UI

### 1.4 Intended Audience

* Product engineers
* Backend and infrastructure developers
* QA and automation engineers
* Technical stakeholders

---

## 2. Overall Description

### 2.1 Product Perspective

The platform is a distributed system consisting of:

* Browser Extension (Recording Layer)
* Web Dashboard (Management Layer)
* Orchestration Service (Queue & Scheduler)
* Execution Workers (Playwright)
* Data Storage & Observability Stack

Each component is loosely coupled and horizontally scalable.

### 2.2 User Classes

* **Standard User**: Records and runs workflows
* **Power User**: Parameterizes workflows and schedules jobs
* **Admin**: Manages workers, queues, and system health

### 2.3 Operating Environment

* Browser Extension: Chromium-based browsers
* Backend: Linux containers
* Execution Engine: Playwright
* Database: Relational (PostgreSQL or equivalent)
* Queue: Redis / SQS / RabbitMQ (pluggable)

### 2.4 Constraints

* CAPTCHA-protected or heavily bot-guarded websites are not supported
* Requires JavaScript-enabled websites
* Network-dependent execution reliability

---

## 3. System Features and Functional Requirements

### 3.1 Browser Interaction Recording

**Description**: Record real user actions on websites

**Functional Requirements**:

* Capture clicks, inputs, navigation, scrolls, and selections
* Record stable DOM selectors with fallbacks
* Timestamp and order all actions
* Support pause, resume, and stop recording
* Store raw recording locally before upload

---

### 3.2 Workflow Generation and Versioning

**Description**: Convert recordings into structured workflows

**Functional Requirements**:

* Transform actions into deterministic steps
* Assign unique workflow IDs
* Maintain immutable versions per edit
* Allow rollback to previous versions

---

### 3.3 Workflow Management Dashboard

**Description**: Central UI for managing workflows

**Functional Requirements**:

* View workflow steps in readable format
* Edit selectors, delays, retries, and timeouts
* Parameterize inputs (variables)
* Enable/disable steps
* Clone workflows

---

### 3.4 Job Scheduling and Triggering

**Description**: Control workflow execution

**Functional Requirements**:

* Manual execution trigger
* Time-based scheduling (cron-like)
* Ad-hoc parameter injection at runtime
* Job enqueueing with metadata

---

### 3.5 Job Queue and Orchestration

**Description**: Reliable job distribution

**Functional Requirements**:

* Centralized job queue
* FIFO processing with priority support
* Retry failed jobs based on policy
* Dead-letter queue for hard failures

---

### 3.6 Workflow Execution Engine

**Description**: Deterministic execution using Playwright

**Functional Requirements**:

* Spin up isolated headless browser per job
* Replay steps sequentially
* Enforce per-step timeouts
* Support retries with backoff
* Abort on unrecoverable errors

---

### 3.7 Data Extraction and Normalization

**Description**: Extract structured data

**Functional Requirements**:

* Extract text, attributes, tables, and lists
* Support multiple selectors per field
* Normalize outputs to JSON
* Validate extracted data schema

---

### 3.8 Observability and Debugging

**Description**: Provide transparency into execution

**Functional Requirements**:

* Capture execution logs per step
* Store screenshots on failure and success
* Track job states (queued, running, failed, completed)
* Provide execution timeline

---

### 3.9 Results Storage and Access

**Description**: Persist and present results

**Functional Requirements**:

* Store results per job execution
* Display results in tabular UI
* Allow CSV/JSON download
* Maintain historical runs

---

## 4. Non-Functional Requirements

### 4.1 Reliability

* Deterministic execution only
* No AI-guess-based interactions
* Idempotent job retries

### 4.2 Scalability

* Horizontal scaling of workers
* Queue-based load distribution
* Stateless execution nodes

### 4.3 Performance

* Job startup under configurable threshold
* Parallel job execution support

### 4.4 Security

* Isolated browser environments
* No credential persistence unless encrypted
* Role-based access control

### 4.5 Observability

* Centralized logging
* Metrics for job duration and failure rate
* Health checks for workers

### 4.6 Maintainability

* Modular services
* Clear separation of concerns
* Versioned APIs

---

## 5. System Architecture Overview

### 5.1 High-Level Flow

1. User records workflow via extension
2. Workflow stored and versioned
3. User triggers or schedules execution
4. Job enters queue
5. Worker consumes job
6. Playwright executes workflow
7. Data extracted and stored
8. Results displayed in dashboard

---

## 6. Assumptions and Dependencies

* Target websites are accessible without advanced bot protection
* Users understand basic browser interactions
* Stable DOM structure for recorded sites

---

## 7. Future Enhancements (Out of Scope)

* Visual selector healing
* AI-assisted selector suggestions
* Distributed browser farms
* Workflow marketplace

---

## 8. Acceptance Criteria

* Users can record, edit, and run workflows without code
* Jobs execute deterministically
* Results are reproducible and auditable
* System scales with additional workers

---

**End of Document**
