# C++/Python Hybrid Architecture Network (CyHAN)
# Standard v1.0

---

## Document Control

**Title:** C++/Python Hybrid Architecture Network (CyHAN) Standard v1.0  
**Status:** Initial Release  
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

```
Desktop Client (Qt C++)
or
Web Client (React / Browser)
│
▼
Python API
▼
Python Orchestration
▼
C++ Engines
```

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

```
Client (Request)

↓

API Layer
• Schema validation
• Authentication and authorization
• Request dispatch

↓

Orchestration Layer
• Workflow construction
• Dependency resolution
• Engine coordination

↓

C++ Engines
• Deterministic numerical computation

↓

Orchestration Layer
• Result aggregation
• Post-processing
• Metadata enrichment

↓

API Layer
• Serialization
• Response emission

↓

Client (Response)
```

All compute **SHALL** follow this sequence.

---

## 6. Deployment Models

### 6.1 Desktop Mode

```
Desktop Client → API → Orchestration → C++ Engines
```

Changing deployment environment **SHALL** require only a configuration change.

---

### 6.2 Cloud Mode

```
Web Client → API → Orchestration → C++ Engines
```

Backend services may be containerized and horizontally scalable.

---

### 6.3 CLI Mode

```
Command-Line Interface → Orchestration → C++ Engines
```

CLI **MAY** bypass API layer but **MUST NOT** bypass orchestration.

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

```
project-root/
│
├── backend/
│  
├── frontend/
│  
├── docs/
│  
├── ...
```

Backend is canonical.  
Frontends are adapters.

---

## 9. Prohibited rchitectural Anti-Patterns

The following practices violate CyHAN Standard v1.0:

- Direct Desktop Client → C++ Engine invocation  
- Direct Web Client → C++ Engine invocation  
- Parallel orchestration stacks for desktop and cloud deployments  
- Numerical kernels embedded within UI layers  
- Multiple or forked execution paths that bypass orchestration  
- Duplication of backend logic across clients

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

---

## 14. Terminology Rationale

The name **C++/Python Hybrid Architecture Network (CyHAN)** is deliberate.  
Each term conveys a specific structural property of the system.

---

### 14.1 Why "Hybrid"

CyHAN is *hybrid* because it intentionally combines multiple computational paradigms within a single coherent execution model.

The hybridization occurs along three dimensions:

#### Language Hybridization
- **C++** provides high-performance, memory-efficient, numerically intensive computation.
- **Python** provides orchestration, workflow governance, integration, and API control.

Each language operates within clearly defined boundaries. Neither replaces the other.

#### Deployment Hybridization
- Native desktop execution (Qt C++)
- Cloud-based web deployment (React / Browser)
- Command-line execution

All share the same backend execution path.

#### Execution Hybridization
- Compiled native engines for performance
- Dynamic orchestration for flexibility
- Controlled stochastic modeling with reproducible execution semantics

Hybrid does not imply fragmentation.  
It implies intentional integration of complementary capabilities.

---

### 14.2 Why "Architecture"

CyHAN is an *architecture* because it defines structural rules governing:

- Layer boundaries
- Authority separation
- Execution flow
- Responsibility ownership
- Compliance constraints

An architecture specifies:

- What each layer may do
- What each layer must not do
- How components interact
- Where authority resides

CyHAN is not a framework or a library.  
It is a structural doctrine governing system composition.

The defining architectural principle is the **single canonical execution path**:

```
Client → Python API → Python Orchestration → C++ Engines
```

All compliant systems must respect this structure.

---

### 14.3 Why "Network"

CyHAN is a *network* because it connects multiple independent components through well-defined boundaries while preserving execution unity.

The network dimension includes:

#### Multi-Client Network
- Qt Desktop client
- Web client
- CLI client
- Automation clients

#### Service Network
- API layer
- Orchestration layer
- Distributed compute workers
- Engine modules

#### Execution Network
Requests traverse a defined sequence of connected layers, forming a structured computational network.

"Network" does not imply internet transport alone.  
It reflects structured interconnection across:

- Languages
- Processes
- Deployment environments
- Compute nodes

CyHAN systems may operate locally, on-premise, or in distributed cloud environments while maintaining architectural integrity.

---

### 14.4 Summary

- **Hybrid** describes intentional multi-paradigm integration.
- **Architecture** describes enforced structural doctrine.
- **Network** describes connected, layered computational composition.

Together, the name reflects a unified, execution-consistent system design rather than a collection of tools.

---

## 15. Recommended Folder Structure

CyHAN prescribes a structural separation between backend authority and frontend adapters.  
The folder structure below reflects the canonical layering model.

This structure is recommended for all CyHAN-compliant implementations.

---

### 15.1 Canonical Layout

```
project-root/
│
├── backend/
│   ├── api/
│   │   └── python/
│   ├── orch/
│   │   └── python/
│   └── engines/
│       └── cpp/
│
├── frontend/
│   ├── desktop/ 
│   └── web/
│
├── docs/
│   └── CyHAN-Standard-v1.0.md
│
└── tests/
```

---

### 15.2 Layer Mapping

The directory layout directly mirrors the architectural layers:

| Folder | Architectural Layer |
|---------|--------------------|
| `backend/api/python` | Python API Layer |
| `backend/orch/python/` | Python Orchestration |
| `backend/engines/cpp/` | C++ Engines |
| `frontend/desktop/` | Qt Desktop Application |
| `frontend/web/` | Web Frontend |

The filesystem SHALL reflect the architectural separation of concerns.

---

### 15.3 Backend Authority

The `backend/` directory is canonical.

It SHALL:

- Contain the authoritative execution path  
- Enforce API → Orchestration → Engine flow  
- Remain frontend-agnostic  
- Contain no UI logic  

Frontend directories SHALL NOT contain business logic or numerical kernels.

---

### 15.4 Engine Isolation

The C++ engine layer SHALL:

- Be isolated under `backend/engines/cpp/`  
- Avoid dependencies on frontend directories  
- Avoid HTTP or UI imports  
- Remain portable and independently testable  

Bindings (if used) SHALL not collapse layer boundaries.

---

### 15.5 Frontend Adapters

Frontend directories are adapters to the backend.

They MAY include:

- UI rendering code  
- Visualization utilities  
- Local configuration  

They SHALL NOT include:

- Orchestration logic  
- Numerical kernels  
- Alternate execution paths  

---

### 15.6 Structural Doctrine

The filesystem is not arbitrary.

It encodes architectural doctrine:

- Backend is authoritative.
- Frontends are clients.
- Engines are isolated.
- Orchestration is centralized.

The folder structure reinforces execution discipline and prevents architectural drift.

### 15.7 Optional Extensions

Implementations MAY include additional directories such as:

```
├── scripts/
├── infrastructure/
├── docker/
├── ci/
├── config/
```

Such additions SHALL NOT violate the canonical execution hierarchy.

---
