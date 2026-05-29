# WSL2 Installation Journey on Windows 10

## Introduction

As part of building a cloud-native and AI-assisted SaaS platform, I needed a proper Linux-based development environment for Docker, containerization, backend development, and future Kubernetes workflows.

The target stack includes:

* ASP.NET Core
* Docker
* Multi-Tenant SaaS Architecture
* AI-assisted development workflow
* Cloud-native infrastructure

For this reason, WSL2 (Windows Subsystem for Linux 2) became the first foundational step.

---

# Initial Installation Attempt

The first installation attempt was executed using:

```powershell
wsl --install
```

At first, Windows started installing:

* Virtual Machine Platform
* Windows Subsystem for Linux

However, during installation, the following error occurred:

```text
Installing: Windows Subsystem for Linux
Catastrophic failure
```

---

# Root Cause Investigation

To investigate the issue, system virtualization status was checked using:

```powershell
systeminfo
```

The result confirmed that virtualization support was enabled:

```text
Hyper-V Requirements:
A hypervisor has been detected.
```

This meant:

* BIOS virtualization was enabled
* Hyper-V support existed
* CPU virtualization was supported
* The problem was likely caused by a corrupted or partial WSL installation

---

# WSL Repair Process

Several repair steps were attempted.

## Disabling WSL Features

The following Windows features were disabled:

```powershell
dism /online /disable-feature /featurename:Microsoft-Windows-Subsystem-Linux /norestart

dism /online /disable-feature /featurename:VirtualMachinePlatform /norestart

dism /online /disable-feature /featurename:Hyper-V /norestart
```

The system was restarted afterward.

---

## Re-Enabling Required Features

After reboot, the required features were enabled again:

```powershell
dism /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

dism /online /enable-feature /featurename:Hyper-V /all /norestart
```

Another reboot was performed.

---

# Successful Ubuntu Installation

Instead of using the older installation flow, Ubuntu was installed directly using:

```powershell
wsl --install -d Ubuntu
```

This time the installation completed successfully:

```text
Distribution successfully installed.
Launching Ubuntu...
Provisioning the new WSL instance Ubuntu
```

---

# Linux User Creation

During provisioning, the first username attempt failed because Linux usernames must follow specific rules.

Invalid example:

```text
Persian characters
```

Valid example:

```text
shain
```

After creating the Linux user successfully, Ubuntu shell became available.

---

# SSH Authentication Setup for GitHub

After WSL installation, GitHub repository cloning initially failed because GitHub no longer supports password authentication over HTTPS.

Error received:

```text
Password authentication is not supported for Git operations.
```

---

# Generating SSH Keys

An SSH key was generated using:

```bash
ssh-keygen -t ed25519 -C "shaindevops@gmail.com"
```

At first, the key was accidentally saved with a custom filename (`default`) instead of the standard location.

This caused:

```bash
ssh-add ~/.ssh/id_ed25519
```

to fail because the expected key file did not exist.

The incorrect files were removed and the SSH key generation process was repeated properly using the default path.

---

# Starting SSH Agent

SSH Agent was started:

```bash
eval "$(ssh-agent -s)"
```

Then the SSH key was added:

```bash
ssh-add ~/.ssh/id_ed25519
```

---

# Connecting GitHub via SSH

The public key was copied using:

```bash
cat ~/.ssh/id_ed25519.pub
```

and added to GitHub SSH Keys settings.

During first SSH connection, GitHub authenticity verification appeared:

```text
The authenticity of host 'github.com' can't be established.
```

After accepting the fingerprint using:

```text
yes
```

authentication succeeded successfully.

---

# Successful GitHub Authentication

Final confirmation:

```text
Hi shaindevops! You've successfully authenticated
```

This confirmed that:

* SSH authentication works
* GitHub access is configured correctly
* WSL environment is operational
* Linux-based development workflow is ready

---

# Lessons Learned

## Key Technical Takeaways

* WSL installation failures are often caused by partial Windows feature corruption
* Hyper-V and virtualization support are critical for WSL2
* Linux usernames follow strict naming rules
* GitHub password authentication is deprecated
* SSH-based authentication is the correct long-term workflow
* Linux-first development environments provide better compatibility for:

  * Docker
  * Kubernetes
  * Cloud tooling
  * AI-native engineering workflows

---

# Final Result

The system is now prepared for:

* Docker development
* ASP.NET Core backend development
* AI-assisted coding workflows using Cursor
* Multi-tenant SaaS development
* Future Kubernetes and cloud-native infrastructure
