
# AI/ML Internship - Task 4: Responsible AI General Health Chatbot

## 📌 Task Objective
The goal of this project is to implement a domain-restricted health education assistant powered by Large Language Models (LLMs) via advanced prompt engineering. The implementation demonstrates how to enforce rigorous safety limits on generative foundations—ensuring helpful general health guidance while completely neutralizing risks related to unauthorized medical prescribing, clinical diagnoses, or improper triage handling.

---

## 🏗️ Safety System Architecture
The application architecture relies on an integrated **Dual-Layer Defense Sandbox** designed to capture vulnerabilities prior to and during active token processing:

1. **The Python Layer (Hard Guardrails):** Programmatically scans raw string content local-side. Detection of key acute medical terms (e.g., *heart attack*, *stroke*, *chest pain*) intercepts execution, completely bypassing external LLM processing to prevent hallucinations and deliver a predefined, immediate emergency alert.
2. **The Prompt Engineering Layer (Soft Guardrails):** Configures an authoritative, empathetic system persona via strict instruction matrices. Llama-3.1 is explicitly prohibited from outlining medication quantities, providing diagnostic assertions, or overriding general educational scopes.

---

## 📊 Technical Configurations & Dataset Profile
* **Core Engine Pipeline:** `meta-llama/Llama-3.1-8B-Instruct` routed via Hugging Face API Endpoints.
* **Interface Layer:** Interactive Jupyter UI Dashboard engineered with `ipywidgets` and custom contextual CSS markdown visualization containers.
* **Authentication Method:** Secure background execution loading via decoupled environment states (`python-dotenv`).

---

## 🏆 Verification Profiles & Crucial Findings

The model was subjected to edge-case verification runs to evaluate structural robustness:
* **Wellness Resolution Check:** When asked about stress minimization protocols, the bot generated highly informative lifestyle recommendations accompanied by mandatory advisory notifications.
* **Emergency Isolation Check:** Queries containing symptoms such as acute chest discomfort successfully triggered local hard intercept blocks. The API execution line dropped out, and the UI correctly rendered high-contrast orange alert indicators directing the user to professional medical care.
* **Dietary Guidance Resolution:** The system responded to nutritional inquiries with well-structured health insights while strictly avoiding specific medical prescriptions.

### 💡 Core Engineering Takeaway
Relying solely on system prompts for security leaves software open to prompt injections and alignment drifting. This project demonstrates that combining deterministic code boundaries (Python filters) with heuristic text generation frameworks (LLMs) provides a reliable method for deploying generative models in highly regulated sectors like healthcare.
