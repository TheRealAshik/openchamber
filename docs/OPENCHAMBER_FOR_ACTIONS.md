# 🚀 OpenChamber for Actions

**Version:** `v0.1.0-preview`  
**Status:** Preview

OpenChamber for Actions lets you run a **full OpenChamber environment in the cloud** using GitHub Actions.  
It provides OpenCode, OpenChamber, and a web-based terminal — **no local hardware required**.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Key Features](#key-features)
- [Quick Start](#quick-start)
- [Beginners' Guide](#beginners-guide)
- [Installation Guide](#installation-guide)
- [FAQ](#frequently-asked-questions-faq)
- [Technical Specifications](#technical-specifications)

---

## Overview

OpenChamber for Actions works like a **temporary cloud computer** powered by GitHub-hosted runners.  
During execution, it starts the following services:

- **OpenCode Web UI** — browser-based development interface  
- **OpenCode TTY** — web-accessible terminal  
- **OpenChamber Core** — main runtime service  

### Runtime Access
> URLs are printed in the workflow logs once the job starts.

### Default Usernames
> [!IMPORTANT]
> These are **usernames only**, not passwords.
>
> - **OpenCode TTY:** `user`  
> - **OpenCode Web:** `opencode`

### Security & Persistence
Services are exposed using secure tunnels (Cloudflare or Ngrok).  
Session data can be stored using GitHub Artifacts.

> [!WARNING]
> **Password authentication is currently not functional.**  
> This will be fixed in a future update.  
>
> **Until then:**  
> - Use this workflow **only in private repositories**  
> - **Do not** rely on `OPENCODE_SERVER_PASSWORD`  
> - Avoid exposing public URLs with sensitive data  

---

## Key Features

| Feature | Benefit |
|------|------|
| Cloud-based | Runs fully on GitHub Actions |
| AI Integration | Antigravity model support (Gemini, Claude) |
| Tunnel Access | Secure browser-based access |
| Session Restore | Artifact-based persistence |
| Auto Monitoring | Self-healing tunnel checks |
| Cross-device | Works on desktop and mobile |

---

## Quick Start

1. **Fork** this repository  
2. Ensure the fork is **private**  
3. **Run** the workflow  
4. **Open** the URLs from workflow logs  

> [!CAUTION]
> Until password support is fixed, **do not run this in public repositories**.

---

## Beginners' Guide

<details>
<summary><b>What is this and who is it for?</b></summary>

### What is OpenChamber for Actions?
It’s a short-lived development environment running on GitHub’s infrastructure instead of your local machine.

### What do I need?
- A GitHub account  
- A modern browser  
- No server, GPU, or local setup  

### Why Cloudflare by default?
Cloudflare Quick Tunnels require no account or API key and provide HTTPS automatically.

### What does persistence mean?
Some session state can be stored as GitHub Artifacts and restored on the next run.

</details>

---

<details>
<summary><b>Usage Limits & Quotas</b></summary>

| Limit | Value | Notes |
|----|----|----|
| Max runtime | 6 hours | GitHub hard limit |
| Artifact size | 2 GB | Per repository |
| Concurrency | 1 run | Prevents conflicts |
| Hardware | 2 vCPU / ~7GB RAM | Standard runner |
| Retention | 90 days | GitHub default |

</details>

---

## Installation Guide

### Option A: Easy Mode (Cloudflare) — Recommended

1. Fork the repository (keep it **private**)  
2. Open the **Actions** tab  
3. Select **OpenChamber for Actions**  
4. Run the workflow with default options  
5. Wait ~30 seconds  
6. Check the **Monitor & Self-Heal** step for URLs  

> [!TIP]
> No configuration is required for Cloudflare tunnels.

---

### Option B: Pro Mode (Ngrok)

<details>
<summary><b>Ngrok setup</b></summary>

#### Step 1: Get Ngrok token
- Sign in to Ngrok  
- Copy your authtoken  

#### Step 2: Add GitHub secret
- Name: `NGROK_AUTH_TOKEN`  
- Value: your token  

#### Step 3: Run workflow
- Select `ngrok` as tunnel provider  
- URLs appear in workflow logs  

</details>

---

## Frequently Asked Questions (FAQ)

<details>
<summary><b>Is this free?</b></summary>

It uses your GitHub Actions minutes:
- Private repos: 2,000 minutes/month  
- Public repos: unlimited  

</details>

<details>
<summary><b>Why does it stop after a few hours?</b></summary>

GitHub enforces a **6-hour job limit**.  
The environment shuts down automatically.

</details>

<details>
<summary><b>Can I use it on mobile?</b></summary>

Yes. Any modern mobile browser works.

</details>

<details>
<summary><b>Is my data secure?</b></summary>

For now:
- Use a **private repository**
- Do not expose public URLs
- Avoid sensitive data in logs

</details>

<details>
<summary><b>Connection refused?</b></summary>

Try:
1. Waiting 30 seconds and refreshing  
2. Checking workflow logs  
3. Restarting the workflow  

</details>

---

## Technical Specifications

<details>
<summary><b>System</b></summary>

| Component | Specification |
|----|----|
| OS | Ubuntu 22.04 |
| CPU | 2 cores (x86_64) |
| RAM | ~7 GB |
| Disk | ~14 GB (ephemeral) |

</details>

<details>
<summary><b>Network & Ports</b></summary>

| Service | Port |
|----|----|
| OpenCode Web | 3000 |
| OpenCode TTY | 7681 |
| Tunnel | 8080 |

</details>

<details>
<summary><b>Security</b></summary>

| Feature | Status |
|----|----|
| Password Auth | ❌ Not working (temporary) |
| Artifact Encryption | Available |
| Tunnel Security | TLS |
| Session Isolation | Full |

</details>

---

> [!WARNING]
> **Legal Notice**
>
> This project is for **educational and development purposes only**.  
> Do not use it for mining, abuse, or any activity violating GitHub policies.

> [!TIP]
> Workflow logs are the authoritative source for runtime status and access URLs.