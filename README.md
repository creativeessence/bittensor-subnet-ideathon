# Semantic Video Moment Retrieval (SVMR) Subnet

> A Bittensor subnet for decentralized semantic video moment retrieval.

---

## Overview

The **Semantic Video Moment Retrieval (SVMR) Subnet** enables semantic search over video content by mapping natural-language scene descriptions to precise timestamp intervals within a video.

This subnet is built on **Bittensor** and leverages its native incentive mechanism to reward miners that produce high-quality semantic interpretations of video segments. Validators evaluate miner performance using synthetic tasks and assign on-chain weights accordingly.

The subnet is designed to be:
- Decentralized
- Multimodal (vision, audio)
- Incentive-aligned
- Resistant to spam and reward gaming

---

## Problem Statement

Users often remember *what happens* in a video, but not *when it happens*.

Existing tools rely on metadata, subtitles, or manual chaptering and cannot reliably answer semantic queries such as:

> "the scene where two generals fight each other with guns"

The SVMR subnet solves this problem by enabling semantic video moment retrieval in a decentralized, competitive environment.

---

## Objective

The objective of this subnet is to:

- Accept a video and a natural-language scene description
- Identify one or more relevant timestamp intervals
- Rank results by semantic relevance
- Incentivize miners that consistently return accurate results

---

## Request Types

The subnet processes two categories of requests.

### Organic Requests

**Source:** End users (API or web UI)

**Purpose:**
- Serve real-world user queries
- Demonstrate product utility

**Incentives:**
- Organic requests **do not affect miner rewards or weights**

**Characteristics:**
- No guaranteed ground truth
- May be ambiguous or noisy

---

### Synthetic Requests

**Source:** Validators

**Purpose:**
- Evaluate miner performance
- Drive incentive allocation

**Incentives:**
- Synthetic requests are the **only** inputs used for miner scoring

**Characteristics:**
- Programmatically generated
- May use known videos, controlled prompts, or consistency heuristics
- Indistinguishable from organic requests to miners

---

## Inputs and Outputs

### Inputs

Each request includes:
- A video reference or video-derived features
- A natural-language description of a target scene
- Optional constraints (e.g. segment duration, modality hints)

---

### Outputs

Miners return ranked timestamp intervals:

```json
{
  "results": [
    { "start": 3720.5, "end": 3812.3, "score": 0.91 },
    { "start": 1840.2, "end": 1901.7, "score": 0.63 }
  ]
}
```

Each interval represents a candidate moment corresponding to the query.

---

## Architecture

```
User / Client
   │
   ▼
Validator
   ├─ Synthetic evaluation (scoring & weights)
   └─ Organic query routing (no incentives)
   │
   ▼
Miners
   └─ Semantic video analysis
```

---

## Roles

### Miners

**Responsibilities:**
- Perform semantic analysis of video segments
- Use vision, audio, or multimodal models
- Return timestamp intervals ranked by relevance

**Constraints:**
- Cannot distinguish synthetic vs organic requests
- Do not assign scores or weights
- Do not receive ground truth

---

### Validators

**Responsibilities:**
- Generate synthetic evaluation tasks
- Query miners and collect responses
- Score miner outputs
- Set on-chain miner weights
- Serve organic user queries (without updating weights)

Validators do **not** distribute rewards directly; they only set weights.

---

## Incentive Mechanism

- Miners respond to all requests identically
- Validators score miners exclusively on synthetic requests
- Validator scores are converted into on-chain weights
- Bittensor’s native mechanism distributes rewards proportionally

The subnet does not override or modify Bittensor’s emissions logic.

---

## Evaluation Criteria

Miner performance may be evaluated using:
- Semantic similarity
- Temporal Intersection-over-Union (IoU)
- Cross-query consistency
- Precision vs recall balance
- Optional latency penalties

Exact scoring functions are validator-defined and deterministic.

---

## Scope

### In Scope
- Semantic video understanding
- Multimodal embeddings
- Temporal scene localization
- Decentralized evaluation and incentives

### Out of Scope
- Video hosting or streaming
- Copyright enforcement
- Video generation or editing
- Centralized indexing of user content

All video content remains user-provided; the subnet operates only on derived representations.

---

## Security Considerations

The subnet mitigates abuse by:
- Separating organic traffic from incentive signals
- Using validator-generated synthetic tasks
- Preventing miners from identifying reward-relevant queries

Additional defenses may be implemented at the validator level.
