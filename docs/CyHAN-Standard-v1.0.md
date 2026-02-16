# C++/Python Hybrid Architecture Network (CyHAN)
# Standard v1.0

---

## Document Control

**Title:** C++/Python Hybrid Architecture Network (CyHAN) Standard v1.0  
**Status:** Approved – Initial Release  
**Scope:** Desktop and Cloud Scientific Computing Platforms  
**Audience:** System architects, HPC developers, scientific software engineers, technical leadership  

---

## 1. Purpose

The **C++/Python Hybrid Architecture Network (CyHAN)** (pronounced **“cyan”**) establishes a unified computational architecture with a single canonical execution path and reproducible execution semantics for high-performance scientific and engineering platforms.

This standard defines:

- Layer boundaries  
- Execution topology  
- Responsibility isolation  
- Deployment models  
- Compliance requirements  
- Architectural constraints  

CyHAN is intended for long-lifecycle technical systems where correctness, scalability, and maintainability are critical.

---

## 2. Problem Statement

Scientific and engineering platforms frequently diverge due to:

- Separate desktop and cloud implementations  
- Duplicate orchestration logic  
- Direct UI-to-engine coupling  
- Inconsistent execution semantics  
- Fragmented deployment models  

Such divergence leads to:

- Non-reproducible results  
- Increased maintenance burden  
- Scaling limitations  
- Hidden technical debt  

CyHAN eliminates divergence by enforcing:

- A single backend execution path  
- Strict separation of UI, orchestration, and compute  
- Clear authority boundaries between layers  

CyHAN is compute-first, not UI-first.

---

## 3. Canonical Architecture

### 3.1 Execution Topology

Qt Desktop Application (Qt C++)
Web Frontend (React / Browser)
│
▼
Python API Layer
▼
Python Orchestration
▼
C++ Engines

All compute **MUST** traverse this stack.

There SHALL be no alternate execution path in compliant systems.

---

### 3.2 Architectural Ordering Rationale

The ordering reflects:

- Native-first engineering philosophy  
- C++ as numerical authority  
- Desktop as primary development environment  
- Web as scalable distribution interface  

Desktop and Web clients are peers. Neither owns computation.

---

## 4. Layer Specifications

---

### 4.1 C++ Engines

#### Role

C++ engines are the sole owners of performance-critical computation.

They **SHALL**:

- Implement numerical kernels  
- Execute Monte Carlo simulation  
- Perform mesh/grid operations  
- Handle memory-intensive workloads  
- Support controlled and reproducible execution  

#### Constraints

C++ engines **SHALL NOT**:

- Expose HTTP endpoints  
- Import UI frameworks  
- Contain workflow orchestration logic  
- Maintain frontend state  

#### Reproducibility

Where stochastic modeling is used:

- Random number generators **MUST** be seed-controlled  
- Execution order **SHOULD** be stable  
- Numerical behavior **MUST** be consistent across deployment modes  

This requirement refers to execution reproducibility, not deterministic hazard modeling philosophy.

---

### 4.2 Python Orchestration Layer

#### Role

Python Orchestration governs workflow assembly and execution control.

It **SHALL**:

- Validate domain-level inputs  
- Compose engine calls  
- Manage job lifecycle  
- Coordinate distributed workers  
- Perform lightweight post-processing  
- Integrate AI/ML modules  

#### Constraints

Python Orchestration **SHALL NOT**:

- Implement heavy numerical kernels  
- Duplicate engine logic  
- Contain UI rendering code  
- Serve as the public API boundary  

Python coordinates. It does not numerically dominate.

---

### 4.3 Python API Layer

#### Role

The Python API defines the authoritative system boundary.

It **SHALL**:

- Expose stable, documented endpoints  
- Validate input schemas  
- Authenticate and authorize requests  
- Dispatch to orchestration  
- Manage asynchronous execution  

#### Authority

All clients **MUST** communicate exclusively through this boundary.

---

### 4.4 Qt Desktop Application

#### Role

The Qt Desktop Application is a native client adapter.

It **SHALL**:

- Own the GUI event loop  
- Manage window lifecycle  
- Render visualization  
- Communicate with the Python API via HTTP or WebSocket  

#### Constraints

The Qt Desktop Application **SHALL NOT**:

- Directly invoke C++ engines in compliant deployments  
- Contain orchestration logic  
- Replicate backend computation  

HTML inside Qt is optional and does not affect compliance.

---

### 4.5 Web Frontend

The Web Frontend **SHALL**:

- Render UI  
- Submit jobs  
- Monitor execution  
- Visualize results  

It **SHALL NOT**:

- Execute heavy computation  
- Contain orchestration logic  

---

## 5. Execution Standard

### 5.1 Canonical Flow

Client Request
↓
Python API Validation
↓
Orchestration Assembly
↓
Engine Invocation
↓
Post-Processing
↓
Response

All compute **SHALL** follow this sequence.

---

## 6. Deployment Models

### 6.1 Desktop Mode

Qt → Local or Remote API → Orchestration → C++

Changing deployment environment **SHALL** require only a configuration change.

---

### 6.2 Cloud Mode

Browser → Cloud API → Orchestration → Distributed C++

Backend services may be containerized and horizontally scalable.

---

### 6.3 CLI Mode

CLI → Orchestration → C++

CLI **MAY** bypass HTTP but **MUST NOT** bypass orchestration.

---

## 7. Execution Parity

CyHAN enforces **desktop–cloud execution parity**.

Given identical:

- Inputs  
- Configuration  
- Seeds  
- Engine versions  

Desktop and cloud deployments **SHALL** produce equivalent computational results.

---

## 8. Structural Requirements

Minimum compliant structure:

backend/
api/
orchestration/
engines/
cpp/
frontend_desktop/
frontend_web/


Backend is canonical.  
Frontends are adapters.

---

## 9. Prohibited Anti-Patterns

The following violate CyHAN Standard v1.0:

- Direct Qt → C++ engine invocation  
- Web → C++ engine invocation  
- Separate desktop/cloud orchestration stacks  
- UI-embedded numerical kernels  
- Forked execution logic  
- Backend duplication  

---

## 10. Compliance Criteria

A system SHALL be considered compliant if:

- All compute flows through Python Orchestration  
- Clients use the API boundary  
- C++ engines are isolated from UI  
- Desktop and Web share backend semantics  
- Execution parity is preserved  
- Reproducible execution is supported  

---

## 11. Performance Doctrine

- Heavy compute **MUST** reside in C++  
- Python **SHALL** coordinate, not dominate  
- API overhead **SHOULD** be negligible relative to engine runtime  
- Scaling **SHALL** occur at worker or orchestration level  

---

## 12. Versioning

CyHAN follows semantic versioning:

- **MAJOR** — Architectural changes  
- **MINOR** — Backward-compatible enhancements  
- **PATCH** — Clarifications or corrections  

Version 1.0 establishes the canonical unified execution path.

---

## 13. Position Statement

CyHAN is:

- Compute-first  
- Reproducible  
- Multi-frontend  
- Cloud-ready  
- Desktop-native  
- Architecturally unified  

CyHAN is not:

- UI-first  
- Web-only  
- Multi-path  
- Monolithic C++  
- Python-only 
