# **Cognis**

**Machine Learning Engine for Facial Recognition and Identity Inference**

Cognis is a modular, low-latency machine learning engine designed for facial recognition, identity verification, and presence inference.

It provides the core computer-vision and ML pipeline required to detect faces, generate embeddings, compare identities, and make confidence-based decisions in real time. Cognis is built to act as an **intelligence layer** behind applications such as attendance systems, access control, and presence-based analytics.

---

## 🧠 What is Cognis?

Cognis is not a UI product or end-user application.

It is an **ML-first backend engine** responsible for:

* Understanding *who* is present
* Verifying identity through facial features
* Producing reliable, machine-interpretable identity decisions

Cognis can operate independently or as the underlying recognition engine for systems like **Eidon**.

---

## 🎯 Design Goals

* **Accuracy first** — reliable identity resolution over convenience
* **Low latency** — real-time inference suitable for live environments
* **Modularity** — components can be swapped or upgraded independently
* **Scalability** — works from single-device setups to distributed systems
* **Privacy-aware** — biometric handling with responsibility in mind

---

## 🧩 High-Level Architecture

```
Input Image / Frame
        ↓
Face Detection & Alignment (OpenCV)
        ↓
Image Preprocessing & Normalisation
        ↓
Embedding Generation (ML Model)
        ↓
Vector Store & Cache (Redis)
        ↓
Similarity Computation
(Cosine / Manhattan Distance)
        ↓
Confidence & Threshold Evaluation
        ↓
Identity Resolution Output
```

Each stage is isolated to allow tuning, optimisation, or replacement.

---

## ⚙️ Technology Stack

### Core Stack

* **Python** – primary language for ML pipelines and inference services
* **OpenCV** – face detection, alignment, cropping, and preprocessing
* **Redis** – in-memory storage for embeddings, caching, and fast lookups

### Machine Learning Concepts

* Face embeddings (vector representations of facial features)
* Distance-based similarity matching
* Threshold-driven identity decisions

---

## 🧬 Facial Recognition Pipeline

### 1. Input Capture

* Images or video frames from camera-enabled devices
* Supports real-time and batch processing workflows

### 2. Face Detection (OpenCV)

* Locates faces within the frame
* Filters invalid frames (no face, multiple faces if disallowed)
* Ensures minimum size and quality requirements

### 3. Preprocessing

* Cropping and alignment
* Scaling and normalisation
* Colour and orientation correction

This step ensures consistency before embedding generation.

---

## 🧠 Embedding Generation

* Each detected face is converted into a **fixed-length numerical vector**
* Embeddings represent distinguishing facial characteristics
* Raw images are not required once embeddings are generated (configurable)

Embeddings are deterministic for the same identity under normal conditions, allowing robust comparison across time.

---

## 📦 Vector Storage & Caching

* Embeddings are stored in **Redis** for fast, in-memory access
* Supports:

  * Enrolled identity vectors
  * Temporary session vectors
  * Recently seen faces cache

Redis enables low-latency matching without persistent database overhead in the critical path.

---

## 📏 Similarity Matching

Cognis compares embeddings using multiple distance metrics:

### Primary Metrics

* **Cosine Similarity**
  Measures angular similarity between vectors (scale-invariant)

* **Manhattan Distance (L1)**
  Measures absolute differences across dimensions

Using multiple metrics increases robustness and allows validation across edge cases.

---

## 🎚️ Decision Engine

* Similarity scores are evaluated against configurable thresholds
* Matches must exceed confidence requirements to be accepted
* Supports:

  * Single-best match
  * Top-K candidate evaluation
  * Rejection on ambiguity

The decision engine outputs a **confidence-aware identity result**, not just a binary match.

---

## ⏱️ Performance Considerations

Cognis is optimised for:

* Low inference latency
* High-throughput environments
* Repeated recognition scenarios

Techniques include:

* Redis-based caching
* Reuse of recent embeddings
* Short-circuit rejection for low-quality frames

---

## 🔁 Typical Use Flow

1. Frame received from input source
2. Face detected and preprocessed
3. Embedding generated
4. Embedding compared against stored vectors
5. Identity resolved or rejected
6. Result returned to consuming system

---

## 🔐 Privacy, Security & Ethics

Cognis is designed with responsible biometric use in mind:

* Embeddings can be stored instead of raw facial images
* Encryption in transit and at rest (implementation-dependent)
* Explicit enrolment and consent assumed
* Clear separation between identity data and application data
* Supports compliance-focused system designs (e.g. UK/EU GDPR)

Cognis aims to enable **trustworthy identity systems**, not passive surveillance.

---

## 🔌 Integration

Cognis is intended to be integrated as:

* A backend ML service
* An internal engine within a larger platform
* A callable recognition layer for attendance or access systems

Example consumers:

* Attendance platforms (e.g. Eidon)
* Access control systems
* Smart campuses
* Event check-in systems

---

## 🚀 Roadmap (Indicative)

* Pluggable embedding models
* Vector database abstraction layer
* Batch inference support
* Model benchmarking & evaluation tooling
* Explainability & confidence reporting
* Hardware acceleration support

---

## 🧭 Philosophy

Cognis is built around a simple idea:

> **Recognition is not about seeing a face — it’s about resolving identity with confidence.**

Everything in Cognis exists to support that principle.
