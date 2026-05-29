# Installing .NET SDK and Node.js on Ubuntu (WSL2)

## Introduction

After installing WSL2 and Ubuntu on Windows, I needed to prepare the development environment for AI-Native and SaaS development.

In this step, I installed:

* .NET SDK
* Node.js
* npm

inside Ubuntu running on WSL2.

---

# Installing .NET SDK

First, I checked whether .NET was already installed:

```bash id="m22rfj"
dotnet --version
```

The system showed that `dotnet` was not installed.

---

## Install .NET SDK 10

Run:

```bash id="wz24va"
sudo apt-get update && \
sudo apt-get install -y dotnet-sdk-10.0
```

---

## Verify Installation

After installation:

```bash id="7o8w7m"
dotnet --version
```

Expected output:

```bash id="i2ik5t"
10.x.x
```

---

# Installing Node.js and npm

First, check if Node.js exists:

```bash id="0z9w88"
node -v
```

The system showed that Node.js was not installed.

---

## Install Node.js

```bash id="vs3n4k"
sudo apt install nodejs
```

During installation, npm and all required dependencies were also installed automatically.

---

# Verify Node.js and npm

```bash id="a9x11k"
node -v
npm -v
```

Expected output:

```bash id="gk8r8x"
v22.x.x
11.x.x
```

---

# Important Notes

## 1. Why Linux Development Environment Matters

Running development environments inside WSL2 is significantly more stable and professional than using Windows directly, especially for:

* Docker
* Kubernetes
* DevOps
* AI Agents
* Cloud-Native systems
* Backend infrastructure engineering

---

## 2. Documentation is an Engineering Asset

Documenting setup steps and troubleshooting helps:

* rebuild environments faster
* improve AI Agent context awareness
* onboard future team members easily
* create reproducible infrastructure

---

# Current Environment Status

✅ WSL2
✅ Ubuntu
✅ GitHub SSH Authentication
✅ Cursor AI
✅ .NET SDK 10
✅ Node.js
✅ npm

---

# Next Steps

Next phase:

* Install Docker Desktop
* Connect Docker with WSL2
* Create SaaS solution structure
* Initialize Clean Architecture foundation
* Start building the Oil Change SaaS platform

---

# AI-Native Engineering Journey

This repository documents the journey of building a real-world SaaS platform using:

* AI Agents
* Modern software architecture
* Cloud-Native engineering
* AI-assisted workflows
* DevOps practices
* Autonomous development systems
