
```markdown
# Mental Health AI Assistant

An interactive conversational AI web application designed to act as an empathetic support companion. This repository features a fine-tuned causal language model deployed via a clean Streamlit frontend, configured to run either locally or optimized for high-speed cloud execution using Cloudflare Tunnels.

---

## 📋 Project Summary

### 1. Task Objective
The objective of this project was to fine-tune a lightweight, domain-specific text generation model capable of parsing emotional user statements and responding with an empathetic, supportive tone. Additionally, the project established a functional deployment pipeline capable of running on a local machine or leveraging a high-speed cloud GPU (NVIDIA T4 via Google Colab) bridged seamlessly to a public web interface.

### 2. Dataset Used
The model was fine-tuned on conversational dialogue data structured around emotional and mental wellness contexts (modeled after datasets like *Empathetic Dialogues*). 
* **Structure:** The training text feeds into a structured prompt template mapping explicit user emotions and inputs to agent outcomes:
  ```text
  Emotion: <emotion>
  Assistant: Customer :<user text>
  Agent :<model response>

```

* **Characteristics:** The training data heavily trains the system to adopt a comforting tone and leverage open-ended follow-up questions to keep the user engaged in dialogue.

### 3. Models & Technologies Applied

* **Base Large Language Model:** `distilgpt2` (a distilled variant of GPT-2 containing 124 million parameters), utilized due to its low hardware requirements and fast iteration capabilities.
* **Frontend Web Framework:** **Streamlit** was used to implement a dynamic, session-state-aware user interface to render clean user and assistant chat message blocks.
* **Proxy Architecture:** **Cloudflare Tunnels (`cloudflared`)** were integrated to serve the app publicly directly out of a Google Colab instance, bypassing the dynamic JavaScript module drops and cross-origin (CORS) connection blockages experienced with alternative tools.

### 4. Key Results and Findings

* **Infrastructure Pipeline:** The application successfully handles real-time text input and generation streaming. When running locally without a strong dedicated graphics card, the model defaults to execution on the system CPU. Moving the hosting logic to Colab enables sub-second text generation via an active cloud GPU.
* **UI & Proxy Troubleshooting:** Early testing configurations revealed framework errors including duplicate UI element registration exceptions. Deployments using standard Localtunnel setups caused front-end rendering drops due to missing dynamic asset chunks, a critical breakdown resolved entirely by moving to a Cloudflare Tunnel configuration.
* **Text Post-Processing:** Initial raw model inferences revealed a tendency for the attention layers to leak structured training sequence tokens—spitting out literal blocks of structural text such as `Customer :`, `Agent :`, or `Emotion :`. A robust regular expression cleaning loop was integrated inside the application script to filter out these artifacts before the text reaches the user.

---

## 🛠️ Installation & Setup Guide

### Local Environment Installation

To install the package dependencies within a clean, isolated Anaconda virtual environment, execute the following commands in your terminal:

```bash
conda create --name Internship_task python=3.10 -y
conda activate Internship_task
pip install torch transformers streamlit

```

### Running the App via Google Colab Cloud Tunnel

To run the model at maximum speed using cloud resources, paste your code into a notebook, ensure the runtime is set to a GPU (T4), and run the following sequence to install the proxy client and boot the live dashboard:

```bash
# 1. Install the official Cloudflare client binary
!wget [https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb](https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb)
!dpkg -i cloudflared-linux-amd64.deb

# 2. Fire up the application server and generate your live URL bridge
!streamlit run app.py --server.port 8501 --server.enableCORS=false --server.enableXsrfProtection=false & cloudflared tunnel --url http://localhost:8501

```

*Click on the temporary public `.trycloudflare.com` URL printed in the running logs to test your interactive application.*

---

## ⚠️ Current Project Status & Limitations

> **CRITICAL NOTE ON OUTPUT QUALITY:**
> While the deployment pipeline, infrastructure tunneling, interface architecture, and data loading scripts are completely functional, **the model is currently not providing accurate, logical, or reliable answers.**
> Because the `distilgpt2` base model is exceptionally small (124M parameters), it lacks the fundamental logical reasoning capabilities required to carry out contextually sound conversations. The model frequently displays "backstory bleed"—blindly pulling in random, disconnected text fragments from human scenarios in the training set or generating responses entirely unrelated to the current statement.
> **Development is actively ongoing to resolve this.** Future steps include migrating the training pipeline to a more robust open-weight base model (such as `gpt2-medium` at 355M parameters, or implementing a 4-bit quantized LoRA adapter on a modern model like `Qwen-2.5-1.5B-Instruct`) to ground the logic while maintaining the empathetic tone.

```

```
