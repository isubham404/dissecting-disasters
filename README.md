# 🔬 Dissecting Disasters: Practical Cyber Attack Teardowns

[![Security: Defensive](https://img.shields.io/badge/Focus-Detection%20Engineering%20%26%20Analysis-blue.svg)](#)
[![MITRE ATT&CK](https://img.shields.io/badge/Mapping-MITRE%20ATT%26CK-orange.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> Practical, reproducible autopsies of defining security incidents and exploits. Moving beyond post-breach headlines to analyze root-cause mechanics, generate real telemetry artifacts, and construct defensible detection engineering rules.

---

## 🎯 Project Agenda & Mission

Most security breach retrospectives limit their scope to surface-level reporting: estimated damages, compromised record counts, and generalized timelines. 

**Dissecting Disasters** approaches security incidents through the lens of offensive mechanics and blue-team engineering. The objective of this repository is to systematically deconstruct real-world attacks into modular, technical post-mortems backed by isolated reproduction environments, observable forensic artifacts, and concrete mitigations.

### Core Objectives
* **Deconstruct Vulnerability Mechanics:** Analyze how specific flaws operate at the protocol, process, and memory layers.
* **Map Tactical Lifecycles:** Trace complete incident paths using the **MITRE ATT&CK** matrix from Initial Access to Impact.
* **Generate Observable Telemetry:** Capture real event logs (e.g., Sysmon, auditd, web application traces) and network packet captures (PCAPs) associated with malicious behavior.
* **Develop Defensive Signatures:** Provide production-ready detection rules (Sigma, Suricata, YARA) designed to identify attack patterns.
* **Deliver Safe, Version-Pinned Reproducibility:** Package self-contained, isolated sandbox environments (via pinned Docker containers or guided virtual labs) so that historically patched flaws can still be reliably compiled, observed, and studied without risking host stability.

---

## 🧭 The Core Methodology

Every analysis in this series follows a unified engineering workflow:

```
+---------------------+     +---------------------+     +---------------------+
| 1. Root Cause       |     | 2. Pinned Sandbox   |     | 3. Execution &      |
|    Analysis         | --> |    Environment      | --> |    Telemetry Capture|
| (Code/Protocol flaw)|     | (Docker / VM Labs)  |     | (Logs, PCAPs, EDR)  |
+---------------------+     +---------------------+     +---------------------+
                                                                   |
                                                                   v
+---------------------+     +---------------------+     +---------------------+
| 6. Hardening &      |     | 5. Detection        |     | 4. MITRE ATT&CK     |
|    Remediation      | <-- |    Engineering      | <-- |    Lifecycle        |
| (Patches, controls) |     | (Sigma, Suricata)   |     |    Correlation      |
+---------------------+     +---------------------+     +---------------------+
```

---

## 🧪 Practical Reproduction Strategy

Many foundational vulnerabilities have long been patched in modern operating systems and upstream package managers. To ensure every attack remains 100% reproducible today without requiring unpatched host machines, this project relies on two practical pathways:

1. **Version-Pinned Containerization:** Each attack module includes custom Dockerfiles or pinned base images that compile and run the exact historical, unpatched software versions in network-isolated containers.
2. **Dedicated Cloud/VM Lab Blueprints:** For attacks requiring complex multi-node infrastructure or legacy kernels, detailed walkthroughs map directly to available pre-configured virtualization targets (e.g., dedicated TryHackMe or Hack The Box security labs).

---

## 📂 Repository Architecture

The repository is structured to maintain strict separation of concerns across teardowns, lab configurations, and detection engineering artifacts:

```text
dissecting-disasters/
├── .github/                     # Issue templates and contribution workflows
├── attacks/
│   ├── [attack-name]/           # Modular directory per incident/attack
│   │   ├── README.md            # Comprehensive post-mortem & technical analysis
│   │   ├── lab/                 # Isolated reproduction files (pinned Dockerfiles, configs)
│   │   ├── telemetry/           # Sanitized log excerpts, event IDs, and PCAP samples
│   │   └── detection/           # Detection rules (Sigma YAML, Suricata rules, YARA)
├── docs/                        # Reference guides, setup standards, and taxonomies
├── LICENSE                      # Open-source MIT License
└── README.md                    # Main series index and documentation
```

---

## 🧱 Anatomy of a Teardown

Each post-mortem adheres to a standardized six-part structure:

1. **Executive Snapshot:** High-level summary, affected software layers, standard metrics (CVSS), and environmental impact.
2. **Tactical Mapping (MITRE ATT&CK):** Tabular progression aligning attacker tactics, techniques, and procedures (TTPs) with formal industry IDs.
3. **Vulnerability Mechanics:** Code-level or architectural examination of the underlying weakness and why standard security boundaries failed.
4. **Telemetry & Detection Artifacts:** Concrete signatures generated during execution, including host-level process creation logs, authorization failures, and wire-level artifacts.
5. **Hands-On Reproduction Blueprint:** Step-by-step instructions for running the pinned container or guided virtual lab to observe the exploit and inspect system responses.
6. **Remediation & Defense-in-Depth:** Architecture-level mitigations, configuration hardening, least-privilege enforcement, and upstream patch validation.

---

## 🛠️ Prerequisites & Setup

To replicate the included lab blueprints, ensure your local workstation meets the following baseline requirements:

* **Containerization Engine:** [Docker Engine](https://docs.docker.com/engine/) (v20.10+) and [Docker Compose](https://docs.docker.com/compose/) (v2.0+)
* **Packet & Log Analysis:** [Wireshark](https://www.wireshark.org/) / `tcpdump`, `jq`, and standard Unix terminal utilities
* **Virtualization (Optional for OS-level labs):** [VirtualBox](https://www.virtualbox.org/) or [Vagrant](https://www.vagrantup.com/)
* **Network Isolation:** All local lab containers execute strictly within private bridge networks (`127.0.0.1`) with external routing restricted where applicable.

---

## ⚖️ Legal & Ethical Disclaimer

All materials, scripts, reproduction blueprints, and configuration files in this repository are developed strictly for academic research, defensive security engineering, and educational telemetry generation.

* All lab procedures must be conducted within isolated, non-production test environments.
* Deploying these techniques or proof-of-concept scripts against third-party networks, systems, or infrastructure without prior explicit, written authorization from the system owner is illegal and strictly prohibited.
* The maintainers assume no liability for misuse, damages, or unintended consequences resulting from the application of the material provided in this repository.