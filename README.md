# 🏠 Home SOC Lab

> A fully containerized Security Operations Center built with Docker, Alpine Linux, and Wazuh SIEM — designed to simulate real-world attack and detection scenarios in an isolated environment.

---

## 📌 Overview

This project builds a home SOC (Security Operations Center) lab entirely using Docker containers. The goal is to simulate real attacks against isolated target machines and monitor them using a SIEM (Security Information and Event Management) system — mirroring how enterprise security teams operate.

**What this lab demonstrates:**
- Setting up and configuring a production-grade SIEM (Wazuh)
- Isolating environments using Docker networks
- Generating and detecting real attack traffic
- Log collection, analysis, and alert triage
- Writing custom detection rules mapped to MITRE ATT&CK

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────┐
│                  Docker Host (Local Machine)          │
│                                                       │
│   Browser → https://localhost (Wazuh Dashboard)      │
│                    │                                  │
│      ┌─────────────▼──────────────┐                  │
│      │         soc-network         │                  │
│      │  ┌──────────────────────┐  │                  │
│      │  │    wazuh-manager     │  │                  │
│      │  │    wazuh-indexer     │  │                  │
│      │  │    wazuh-dashboard   │  │                  │
│      │  └──────────┬───────────┘  │                  │
│      └─────────────│──────────────┘                  │
│                    │ (bridges both networks)          │
│      ┌─────────────▼──────────────┐                  │
│      │       target-network        │                  │
│      │  ┌────────────────────┐    │                  │
│      │  │  alpine-target-1   │    │                  │
│      │  │  alpine-dvwa       │    │                  │
│      │  │  alpine-attacker   │    │                  │
│      │  └────────────────────┘    │                  │
│      └────────────────────────────┘                  │
└─────────────────────────────────────────────────────┘
```

Two isolated Docker networks:
- **soc-network** — SIEM stack lives here, dashboard exposed to local browser only
- **target-network** — attack targets and attacker container, fully isolated from host

---

## 🛠️ Tools & Technologies

| Tool | Role |
|---|---|
| Docker & Docker Compose | Container orchestration and network isolation |
| Alpine Linux | Lightweight base OS for target and attacker containers |
| Wazuh Manager | SIEM engine — decodes logs and matches detection rules |
| Wazuh Indexer | OpenSearch-based storage for all events and alerts |
| Wazuh Dashboard | Web UI for monitoring alerts (OpenSearch Dashboards) |
| Wazuh Agent | Installed inside targets — ships logs to the manager |
| DVWA | Damn Vulnerable Web Application — web attack target |

---

## 📁 Project Structure

```
home-soc-lab/
├── README.md
├── docker-compose.yml
├── docs/
│   ├── architecture.md       # Detailed network and component design
│   ├── setup-guide.md        # Step-by-step build walkthrough
│   ├── attack-runbook.md     # Attacks simulated and methodology
│   └── findings.md           # Alerts fired, analysis, and lessons learned
├── screenshots/              # Dashboard screenshots and alert captures
├── targets/
│   ├── alpine-target/
│   │   └── Dockerfile
│   └── alpine-dvwa/
│       └── Dockerfile
└── attacker/
    └── Dockerfile
```

---

## 🚀 How to Run This Lab

> Requirements: Docker and Docker Compose installed, minimum 8GB RAM (16GB recommended)

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/home-soc-lab.git
cd home-soc-lab

# Start all containers
docker compose up -d

# Access the Wazuh Dashboard
# Open browser → https://localhost
# Default credentials: admin / SecretPassword
```

_Detailed setup walkthrough in [docs/setup-guide.md](docs/setup-guide.md)_

---

## ⚔️ Attacks Simulated

| Attack | MITRE Technique | ID | Status |
|---|---|---|---|
| SSH Brute Force | Brute Force | T1110 | 🔜 Planned |
| Port Scanning | Network Service Discovery | T1046 | 🔜 Planned |
| Web SQLi (DVWA) | Exploit Public-Facing Application | T1190 | 🔜 Planned |
| New User Creation | Create Account | T1136 | 🔜 Planned |
| Reverse Shell | Command and Scripting Interpreter | T1059 | 🔜 Planned |

_Full attack methodology in [docs/attack-runbook.md](docs/attack-runbook.md)_

---

## 📊 Key Findings

> _This section will be updated as the lab progresses_

- [ ] First alert detected
- [ ] Brute force rule triggered
- [ ] Custom detection rule written
- [ ] MITRE ATT&CK mapping verified

_Detailed findings and analysis in [docs/findings.md](docs/findings.md)_

---

## 📸 Screenshots

> _Dashboard and alert screenshots will be added as the lab is built_

| Stage | Preview |
|---|---|
| Wazuh Dashboard | _Coming soon_ |
| First Alert Fired | _Coming soon_ |
| MITRE ATT&CK View | _Coming soon_ |
| Brute Force Detection | _Coming soon_ |

---

## 🧠 Why I Built This

<!-- Fill this in with your own words as you go -->

_Coming soon — personal motivation and learning goals_

---

## 📖 Key Learnings

> _Updated as the project progresses_

- 
- 
- 

---

## 🗓️ Build Journal

| Date | What I Did |
|---|---|
| 2026-06-14 | Project initialized, repo created, architecture designed |
| | |

_Full journal in [docs/journal.md](docs/journal.md)_

---

## 📚 References & Resources

- [Wazuh Official Documentation](https://documentation.wazuh.com)
- [MITRE ATT&CK Framework](https://attack.mitre.org)
- [Docker Documentation](https://docs.docker.com)
- [DVWA GitHub](https://github.com/digininja/DVWA)

---

## 👤 Author

**Your Name**
- GitHub: [@your-username](https://github.com/your-username)
- LinkedIn: [your-linkedin](https://linkedin.com/in/your-profile)

---

## ⚠️ Disclaimer

This lab is for **educational purposes only**. All attacks are performed inside isolated Docker containers against intentionally vulnerable systems. Never use these techniques against systems you do not own or have explicit permission to test.
