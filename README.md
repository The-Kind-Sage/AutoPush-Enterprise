# AutoPush 🚀
> **Set-and-forget Git automation with intelligent pre-flight alarms, secret shields, and offline auto-syncing.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Security: AES-256-GCM](https://img.shields.io/badge/Security-AES--256--GCM-brightgreen.svg)](#security--compliance)
[![GDPR: Compliant](https://img.shields.io/badge/GDPR-Compliant-blue.svg)](#security--compliance)
[![Vulnerabilities: 0](https://img.shields.io/badge/Vulnerabilities-0%20(Audited)-success.svg)](#penetration-testing--security-audit)

**AutoPush** is an intelligent desktop utility designed for developers, students, and freelancers who want automated backups, consistent commit streaks, and background Git synchronization without manually running `git add`, `git commit`, and `git push` before shutting their laptop.

---

## ✨ Key Features

### ⚡ 1. Dual Push Engines
* **Auto Mode (No Schedule Needed):** Monitors your code in the background. The moment your edits reach your minimum threshold and internet connectivity is verified, it pushes automatically.
* **Scheduled Mode:** Set specific target times (e.g. *Tonight at 11:00 PM*, *Tomorrow Night*, or *Custom Date & Time*).

### 🚨 2. Pre-Flight File Threshold Alarm
* Never push empty or incomplete commits!
* Configure a minimum changed-file threshold (e.g., minimum 2 files). If the scheduled time arrives and fewer than $N$ files are staged, AutoPush **halts the push, sounds an audio alarm, and triggers a desktop alert** asking you to reschedule (+3 hours, tomorrow night, or push anyway).

### 🛡️ 3. Secret & API Key Leak Shield
* Prevents disastrous leaks before code reaches GitHub.
* Scans all staged files for `.env`, AWS access keys, GitHub personal access tokens (`ghp_`), Google API keys, Slack tokens, and private SSH keys (`id_rsa`). If a secret is detected, **the push is immediately aborted**.

### 🌿 4. Safe Branch Mode
* Hesitant about auto-pushing straight to `main`?
* Push directly to an isolated backup branch (e.g. `autopush/backup-laptop`). Your work is safely stored in the cloud without triggering production CI/CD pipelines.

### 🌐 5. Smart Connectivity & Offline Outbox
* Probes DNS connection to `github.com`.
* **When Offline:** Pauses execution safely and queues edits into a local outbox.
* **When Online:** Instantly detects network recovery and synchronizes pending commits.

### 📜 6. Enterprise Cryptographic Audit Trails
* Tracks every user action and automated push with timestamps, actor IDs, and **SHA-256 cryptographic hashes** to ensure organizational accountability and tamper-evident history.

### 📊 7. Analytics & Data Migration
* Built-in visual charts for **7-Day Push Velocity** and **File Distribution**.
* One-click export to **Microsoft Excel (`.xlsx`)**, **CSV**, and **JSON**.

---

## 🖥️ User Interface Preview

AutoPush comes with:
* **Drag-and-Drop Staging Zone:** Drop any local repository folder into the app to inspect branches, untracked files, and remotes.
* **Interactive Staging Checklist:** Check or uncheck exactly which files to include in the commit.
* **Native Desktop Setup Wizard:** Multi-step installer dialog with license agreements, destination selection, and progress bars.
* **Role-Based Access Control (RBAC):** Switch between Administrator, Lead Developer, Contributor, and Compliance Auditor profiles.

---

## 🚀 Getting Started

### Option A: Run the Standalone Desktop Executable (`.jar`)

No complicated installation required!

1. Make sure you have **Java 11 or higher** installed.
2. Download **`AutoPush.jar`**.
3. **Double-click** the file (or run via terminal):
   ```bash
   java -jar AutoPush.jar
   ```

---

### Option B: Run the Web & Daemon Suite (Node.js)

```bash
# 1. Clone repository
git clone https://github.com/your-username/autopush.git
cd autopush/autopush-app

# 2. Install dependencies
npm install

# 3. Start AutoPush Daemon
node server.js
```
Open your browser at `http://localhost:3000`.

---

## 💻 Setting Up Auto-Start on Laptop Boot

To ensure AutoPush runs quietly in the background whenever you open your laptop:

### Windows:
1. Press `Win + R`, type `shell:startup`, and press Enter.
2. Right-click inside the folder $\rightarrow$ **New $\rightarrow$ Shortcut**.
3. Set the target to:
   ```cmd
   javaw -jar "C:\Path\To\AutoPush.jar"
   ```
   *(Using `javaw` ensures it runs in the background without opening a black command prompt window).*

### macOS:
1. Open **System Settings $\rightarrow$ General $\rightarrow$ Login Items**.
2. Click **+** under *Open at Login* and select `AutoPush.jar`.

### Linux (systemd User Service):
Create `~/.config/systemd/user/autopush.service`:
```ini
[Unit]
Description=AutoPush Git Automation Daemon
After=network.target

[Service]
ExecStart=/usr/bin/java -jar /path/to/AutoPush.jar
Restart=always

[Install]
WantedBy=default.target
```
Enable with:
```bash
systemctl --user enable --now autopush.service
```

---

## 🔒 Security & Penetration Testing

AutoPush has undergone security audits and penetration testing:
* **Zero Command Injection (CWE-78):** Parameterized execution dispatches binary arguments directly to the OS kernel without invoking `/bin/sh` or `cmd.exe`.
* **Dynamic Ephemeral Encryption:** Cloud snapshots are secured using **AES-256-GCM** with keys generated at runtime stored in a protected `.master_secret.key` file (`0600` permissions).
* **Strict Path Sanitization:** Rejects path traversal and verifies local `.git` structures before binding directories.
* **Audited Dependencies:** 0 vulnerabilities (`npm audit` clean).

---

## 🛠️ Project Structure

```text
├── AutoPush.jar                     # Standalone compiled desktop application
├── autopush-app/                    # Daemon server & Web dashboard
│   ├── server.js                    # Core daemon, Git executor & scheduler
│   ├── public/                      # Web UI, Chart.js & Setup Wizard
│   │   ├── index.html
│   │   ├── style.css
│   │   └── app.js
│   └── backups_cloud/               # Encrypted AES-256-GCM snapshots
├── autopush-java/                   # Java Swing source code
│   └── src/com/autopush/
│       ├── AutoPushApp.java         # Desktop GUI interface
│       ├── GitService.java          # Parameterized Git process builder
│       ├── InstallerDialog.java     # Setup Wizard dialogue
│       └── ProjectConfig.java       # Configuration model
└── README.md                        # Documentation
```

---

## 📄 License

This project is licensed under the **MIT License** - feel free to use, modify, and distribute it for personal and commercial projects.
