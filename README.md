# ChronoSeek (SVMR Subnet)

> **Semantic search for video moments.**

**ChronoSeek** is a decentralized AI subnet on Bittensor for semantic video moment retrieval, enabling users to locate precise timestamp intervals within videos using natural-language descriptions.

🌐 **Website:** [chronoseek.ai](https://chronoseek.ai/)

---

## 📚 Project Documentation

This project is organized into the following key documents:

- **[Problem Statement](./PROBLEM_STATEMENT.md)**  
  *Why ChronoSeek exists, the "dark data" problem, and the limitations of current search tools.*

- **[System Design](./DESIGN.md)**  
  *Technical architecture for Seekers (Miners) and Chrono Validators, including Incentive Mechanism, Attack Vectors, and Ecosystem Integrations.*

- **[MVP Specifications](./MVP_SPEC.md)**  
  *The "Start Small" launch plan using the ActivityNet dataset to ensure consistency between design and initial testnet behavior.*

- **[Business Logic & Market Rationale](./BUSINESS_LOGIC.md)**  
  *Market size ($94B+), commercialization strategy, and competitive advantage against centralized giants.*

---

## 🚀 Quick Start (Ideathon)

### 1. The Core Concept
We are building a decentralized protocol where:
*   **Seekers (Miners)** use AI models (CLIP, Transformers) to "watch" videos and find specific moments.
*   **Chrono Validators** generate synthetic queries to grade miners and serve organic requests.
*   **Users** get precise timestamps (e.g., "04:12 - 04:18") for natural language queries.

### 2. Architecture Overview
```
User / Client
   │
   ▼
Chrono Validator (Gateway)
   ├─ Synthetic evaluation (scoring & weights)
   └─ Organic query routing
   │
   ▼
Seekers (Miners)
   └─ Semantic video analysis (CLIP / SOTA Models)
```

## 🛠️ Status
*   **Phase:** Ideathon / Design
*   **Current Focus:** Architecture Design, Market Validation, Protocol Definition.

---

## 📜 License
MIT License
