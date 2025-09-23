# privescAPT

**privescAPT** is a post-exploitation enumeration tool inspired by LinPEAS, focused on techniques and artifacts commonly associated with Advanced Persistent Threat (APT) activity.
Its purpose is to help security researchers, red teamers, and incident responders identify suspicious configurations, persistence mechanisms, and traces that often appear in real-world APT intrusions.

> **Disclaimer:** privescAPT is intended strictly for defensive research, threat hunting, incident response, and authorized red-team assessments. Do not run this tool on systems for which you do not have explicit permission. The authors are not responsible for misuse.

---

## Features

* **Persistence enumeration**

  * Scans common persistence vectors (systemd timers, Cron jobs, Windows Scheduled Tasks, Registry Run keys, services).
  * Detects suspicious service binaries, unusual autorun entries, and common hijacking patterns (e.g., DLL search order anomalies) at a high level.

* **Local TTP mapping**

  * Maps observed findings to MITRE ATT\&CK techniques to aid analysis and reporting.
  * Highlights configuration items and artifacts frequently tied to reconnaissance, lateral movement, and privilege escalation.

* **Credential and sensitive data indicators**

  * Looks for unsecured credential stores, credential files left in repositories, and misconfigured token files (only identifies likely indicators; does not attempt credential extraction).
  * Flags evidence of common misconfigurations that could lead to credential exposure.

* **Command and script artifact discovery**

  * Searches for suspicious script files, uncommon scheduled script runners, and persistent launcher patterns.
  * Examines shell profiles and startup scripts for embedded network or execution commands.

* **Logging and forensic hints**

  * Collects locations of relevant logs (PowerShell logs, system logs, audit logs) and points out log gaps or disabled logging which are frequently abused by attackers.

* **Network/communication indicators**

  * Enumerates network sockets and persistent outbound connections, reports unusual listening ports and non-standard proxies.
  * Extracts hostnames and domains from local configuration files and scripts to surface hardcoded C2-like indicators.

* **Reporting**

  * Produces a human-readable plain text report and optional JSON output for automated ingestion into SIEMs and threat-intelligence pipelines.

---

## Supported Platforms

* Linux (bash/sh)
* Windows (PowerShell)
* macOS (limited checks where applicable)

> The tool is modular: platform-specific modules run only when the environment is detected.

---

## Usage

**Linux (example):**

```bash
chmod +x privescAPT.sh
bash privescAPT.sh
```

---

## Project Layout

```
privescAPT/
├── privescAPT.sh           # Linux enumeration script          
└── README.md            # This file
```

---

## How privescAPT Differs from LinPEAS

* **APT-focused indicators:** Emphasis on artifacts and patterns commonly observed in APT investigations (e.g., long-lived stealthy persistence, evidence of living-off-the-land tool abuse, subtle logging configuration changes).
* **TTP correlation:** Built-in mapping of findings to ATT\&CK techniques to speed analyst understanding and reporting.
* **Forensic hygiene awareness:** Avoids destructive or intrusive actions; prioritizes safe, read-only enumeration and collection of trace evidence.

---

## Limitations & Safety

* privescAPT performs **read-only** checks and does not exploit vulnerabilities, extract credentials, or perform destructive changes.
* Due to the diversity of operating environments, **false positives and false negatives** are possible. Findings should be validated with additional forensic or monitoring data.
* Use in production systems may trigger alerts in defensive products. Run in coordination with defenders when used in exercises.

---

## Contributors & Attribution

This project is a community-focused research tool. When adapting or extending the tool, please credit original authors and respect licensing. If you integrate modules from other projects, comply with their licenses.

---

## License

Choose an appropriate license for your project (e.g., MIT, Apache-2.0). The README does not include a license text—add a `LICENSE` file to the repository.

---

## Contact & Reporting

For issues, improvements, or to share non-sensitive findings, open an issue or pull request in the repository. For sensitive disclosures (e.g., discovered vulnerabilities in third-party code or misconfigurations affecting others), follow responsible disclosure procedures and contact affected vendors or administrators directly.

---

## Appendix: Ethics & Responsible Use

This project is intended for legal and ethical security work: authorized red team engagements, incident response, research, and defender tooling. Never use it to access, modify, or persist on systems without express permission. Unauthorized use is illegal and unethical.

---

If you want, I can also:

* Provide a ready-to-paste `LICENSE` (MIT or Apache-2.0).
* Generate a basic `privescAPT.sh` or `privescAPT.ps1` skeleton with safe, non-destructive checks (read-only).
* Create a `ttp-mapping.md` file that pairs common findings with MITRE ATT\&CK IDs.
