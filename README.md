# Semantic Video Moment Retrieval (SVMR) Subnet

> **A Bittensor subnet for decentralized semantic video moment retrieval.**

The **SVMR Subnet** enables semantic search over video content by mapping natural-language scene descriptions to precise timestamp intervals within a video.

---

## 📚 Project Documentation

This project is organized into the following key documents:

- **[Problem Statement](./PROBLEM_STATEMENT.md)**  
  *Why this subnet exists, the "dark data" problem, and the limitations of current search tools.*

- **[System Design](./DESIGN.md)**  
  *Technical architecture, including Miner/Validator logic, Synthetic Task Generation, and SOTA research references (CLIP, LLMs).*

- **[Business Logic & Market Rationale](./BUSINESS_LOGIC.md)**  
  *Market size ($94B+), commercialization strategy, and competitive advantage against centralized giants.*

---

## 🚀 Quick Start (Ideathon)

### 1. The Core Concept
We are building a decentralized protocol where:
*   **Miners** use AI models (CLIP, Transformers) to "watch" videos and find specific moments.
*   **Validators** generate synthetic queries to grade miners and serve organic requests.
*   **Users** get precise timestamps (e.g., "04:12 - 04:18") for natural language queries.

### 2. Architecture Overview
```
User / Client
   │
   ▼
Validator (Gateway)
   ├─ Synthetic evaluation (scoring & weights)
   └─ Organic query routing
   │
   ▼
Miners
   └─ Semantic video analysis (CLIP / SOTA Models)
```

## 🛠️ Status
*   **Phase:** Ideathon / Design
*   **Current Focus:** Architecture Design, Market Validation, Protocol Definition.
