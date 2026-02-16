# C++/Python Hybrid Architecture Network (CyHAN)

## Standard v1.0

CyHAN (pronounced *“cyan”*) establishes a unified computational architecture for high-performance scientific and engineering platforms.

It enforces:

- A single canonical execution path  
- High-performance C++ compute engines  
- Python-based orchestration  
- Authoritative API boundary  
- Native Qt desktop clients  
- Cloud-ready web frontends  
- Desktop–cloud execution parity  

All computation flows through one authoritative backend stack.

---

## Core Architecture

Qt Desktop Application (Qt C++)
Web Frontend (React / Browser)
│
▼
Python API Layer
▼
Python Orchestration
▼
C++ Engines

Both desktop and web clients are peers.

The ordering reflects:

- Native-first design philosophy  
- Performance authority in C++  
- Desktop as the primary engineering environment  
- Web as a scalable distribution interface  

---

## Architectural Principles

### 1. Single Execution Path

All production compute SHALL traverse:

Client → Python API → Python Orchestration → C++ Engines

No client may directly invoke C++ engines in compliant deployments.

---

### 2. Engine Isolation

C++ engines:

- Implement performance-critical numerical kernels  
- Remain deterministic  
- Avoid UI dependencies  
- Avoid HTTP routing  
- Avoid workflow orchestration  

---

### 3. Orchestration Governance

Python orchestration:

- Assembles workflows  
- Coordinates engine calls  
- Manages job lifecycle  
- Performs lightweight post-processing  
- Remains UI-agnostic  

Python coordinates. It does not numerically dominate.

---

### 4. API Contract Authority

The Python API layer:

- Defines the canonical system boundary  
- Exposes versioned endpoints  
- Validates inputs  
- Handles authentication  
- Dispatches to orchestration  

The API governs system semantics.

---

## Layer Responsibilities

### Qt Desktop Application (Native Client)

- Native OS integration  
- Event loop ownership  
- Visualization  
- HTTP client communication with API  

HTML inside Qt is optional and not required by the standard.

---

### Web Frontend (Browser Client)

- UI rendering  
- Job submission  
- Monitoring  
- Visualization  

Web clients communicate exclusively through the API.

---

### Python API

- Endpoint exposure  
- Input validation  
- Authentication  
- Async job handling  
- Dispatch to orchestration  

---

### Python Orchestration

- Workflow assembly  
- Engine coordination  
- Post-processing  
- Metadata management  

---

### C++ Engines

- Numerical solvers  
- Monte Carlo execution  
- Mesh/grid operations  
- Deterministic RNG  
- Parallel compute  

Heavy computation lives here.

---

## Deployment Modes

### Desktop Mode

Qt → localhost API → Orchestration → C++

### Cloud Mode

Browser → Cloud API → Orchestration → Distributed C++

### CLI Mode

CLI → Orchestration → C++

CLI may bypass HTTP but must not bypass orchestration.

---

## Compliance Requirements

A system is CyHAN Standard v1.0 compliant if:

- All compute flows through Python Orchestration  
- API contracts are versioned  
- C++ engines are isolated from UI  
- Desktop and Web share identical backend semantics  
- Deterministic engine execution is preserved  

---

## Performance Doctrine

- Heavy compute MUST remain in C++  
- Python coordinates, not dominates  
- API overhead must be negligible relative to engine execution  
- Scaling occurs at the worker orchestration layer  

---

## Recommended Project Structure

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

## What CyHAN Is

- Compute-first  
- Deterministic  
- Multi-frontend  
- Cloud-ready  
- Desktop-native  
- Architecturally unified  

---

## What CyHAN Is Not

- UI-first  
- Web-only  
- Monolithic C++  
- Python-only  
- Multi-path  

---

For the complete technical specification, see:

`docs/CyHAN-Standard-v1.0.md`
