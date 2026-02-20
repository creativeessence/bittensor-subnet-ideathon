# MVP Specifications: "Proof of Concept" Phase

> **Philosophy:** Dream Big, Start Small.
> This document defines the airtight, minimal viable product (MVP) scope for the ChronoSeek subnet launch.

## 1. MVP Scope Definition

For the MVP, we will narrow the scope to **one** evaluation mode and **one** dataset source to ensure scoring is objective and undeniable.

| Component | Full Vision | MVP Specification |
| :--- | :--- | :--- |
| **Video Source** | Any URL (YouTube/Vimeo) | **Fixed Dataset:** ActivityNet Captions (20k videos) hosted on high-availability CDNs. |
| **Query Type** | Open-ended Natural Language | **Exact Match Retrieval:** Queries are drawn directly from the existing human-verified ActivityNet annotations. |
| **Scoring** | IoU + Latency + Penalties | **Strict IoU:** Only Intersection-over-Union (IoU) > 0.5 counts. No latency weighting yet. |
| **Inference** | Chutes / Decentralized | **Basilica (SN39) Compute:** Miners and Validators utilize Basilica's decentralized GPU marketplace for training and inference during the Hackathon. |

## 2. The "Airtight" Scoring Rubric (MVP)

We avoid synthetic ambiguity by using a **Label-Backed Evaluation** strategy.

### 2.1. The Dataset: ActivityNet Captions
*   **Why:** It is the industry standard for Dense Video Captioning.
*   **Data:** Contains 20,000 videos with 100,000 human-annotated timestamp intervals.
*   **Format:** `(VideoID, Start: 10.5s, End: 20.0s, Sentence: "A man is playing the guitar")`

### 2.2. Task Generation (Deterministic)
Validators do *not* generate new captions. They simply:
1.  Select a random row from the ActivityNet validation set.
2.  Send the `VideoID` and `Sentence` to the miner.
3.  Keep `Start` and `End` hidden as Ground Truth (GT).

### 2.3. Scoring Logic (Binary Threshold)
To remove subjectivity, we use a hard threshold metric: **R@1, IoU=0.5**.

1.  **Miner Output:** Returns one interval `[m_start, m_end]`.
2.  **IoU Calculation:**
    $$ IoU = \frac{\text{Intersection}(Miner, GT)}{\text{Union}(Miner, GT)} $$
3.  **Score Assignment:**
    *   If $IoU \ge 0.5$: **Score = 1.0**
    *   If $IoU < 0.5$: **Score = 0.0**

*Rationale:* This binary scoring prevents "gaming" small overlaps. Either you found the scene, or you didn't.

## 3. MVP Architecture (Simplified)

```
Validator
   │
   ├─ 1. Load ActivityNet JSON (Ground Truth)
   ├─ 2. Pick random (Video, Text) pair
   ├─ 3. Send to Miner
   │
Miner (Local Docker)
   ├─ 1. Receive (Video, Text)
   ├─ 2. Run CLIP-based Sliding Window (Baseline)
   └─ 3. Return [Start, End]
   │
Validator
   └─ 4. If IoU(Response, GT) > 0.5 -> Reward
```

## 4. Why This Works

1.  **Robustness:** Binary Pass/Fail scoring on a known dataset removes all subjectivity.
2.  **Consistency:** By starting with a static dataset, we guarantee that the Testnet behavior matches the design spec 1:1, avoiding the chaos of unproven synthetic generators on Day 1.
3.  **Undeniable Truth:** If a miner complains about a score, we can point to the human-annotated dataset. "The dataset says the guitar solo is at 10s. You said 50s. You are wrong."

## 5. Roadmap to Full Vision
*   **Month 1 (MVP):** ActivityNet Dataset, Strict IoU Scoring, Local Inference.
*   **Month 2:** Add Synthetic Tasks (for new videos) + Latency Scoring + Chutes integration.
*   **Month 3+:** Ecosystem Apps.
