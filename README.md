# Cowrie Honeypot Lab - Network Attack Detection & Reporting

A hands-on lab simulating an external attacker's reconnaissance and unauthorized access attempt against a decoy SSH server, built as Assignment 1 for Bincom Academy's Cybersecurity Class.

## Objective

Build a honeypot, attack it from a separate machine, and capture evidence of the full attack lifecycle - reconnaissance, exploitation attempt, and traffic analysis.

## Lab Architecture

- **Kali Linux** (attacker) - used for scanning and simulated intrusion attempts
- **Ubuntu Server + Cowrie Honeypot** (target) - a decoy SSH service designed to look vulnerable and log all attacker activity

All VMs run in VirtualBox on an isolated lab network.

## Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux | Attacker toolkit |
| Nmap | Port scanning / service enumeration |
| Wireshark | Network traffic capture and analysis |
| Cowrie | SSH/Telnet honeypot |

## Methodology

1. **Reconnaissance** - Ran a full TCP port scan (`nmap -sV -p-`) against the target to identify open ports and running services.
2. **Exploitation attempt** - Attempted SSH logins against the honeypot using varied, non-legitimate credentials, simulating a brute-force/credential-guessing attack.
3. **Traffic capture** - Captured all traffic live in Wireshark during the scan and login attempts.
4. **Evidence review** - Reviewed Cowrie's session logs, which recorded the attacker's source IP, credentials attempted, and commands typed inside the fake shell.
5. **Reporting** - Documented the full incident in a formal incident report (attack summary, technical details, impact assessment, defense recommendations).

## Key Finding

The scan revealed an unexpected second SSH-like service on a non-standard port - a reminder that any unfamiliar open port discovered during a scan should always be investigated, since it may not be what it first appears to be.

## Files in this repo

- `Incident_Report_Assignment1.docx` - full write-up: attack summary, technical details, impact assessment, and defense recommendations
- `honeypot_running.png` - Cowrie honeypot started and listening
- `nmap_scan.PNG` - Nmap scan results showing open ports and services
- `new_wireshark_1.PNG` - Wireshark packet capture of the attack traffic
- `cowrie_log_new.PNG` - Cowrie session logs showing captured credentials and commands
- `cowrie_attack_capture.pcapng` - raw Wireshark packet capture (355 packets)

## Defense Recommendations (summary)

- Disable SSH password authentication in favor of key-based auth
- Deploy fail2ban to rate-limit repeated failed logins
- Restrict SSH access by IP where possible
- Regularly audit open ports to catch unexpected services
- Forward honeypot/SSH logs to a central SIEM for real-time alerting

## Credits

- [Cowrie Honeypot](https://github.com/cowrie/cowrie) — open-source SSH/Telnet honeypot used in this lab (not included in this repo; deployed per their official installation guide)
