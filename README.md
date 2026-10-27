# Smart-Home Cyber-Security and Privacy Baseline (OT Principles Applied at Home)

**The security controls applied across a ~110-integration Home Assistant estate and its public documentation, written as principles and a checklist, in the same spirit as operational-technology (OT) security for building management systems: segment and minimise exposure, control who can command the plant, protect credentials, verify what devices transmit, and publish without leaking. Specific device, network and security-system details are deliberately withheld.**

[![YouTube](https://img.shields.io/badge/YouTube-The%20Control%20Cabinet-red?logo=youtube)](https://www.youtube.com/channel/UC5Cupmz7vlfcodpCX7k8iuQ)
[![Portfolio](https://img.shields.io/badge/Portfolio-the--control--cabinet-24292f?logo=github)](https://github.com/the-control-cabinet)
![Domain](https://img.shields.io/badge/OT%20security-baseline-darkred)
![Status](https://img.shields.io/badge/Status-Live-brightgreen)

> **The short version:**
> - **No inbound ports:** remote access is through an encrypted cloud relay only.
> - **Credentials and transport:** encrypted device APIs, secrets kept out of configs, credential rotation.
> - **Least privilege:** read-only by default, with write access tiered by risk.
> - **Radio links:** the transmit side of a plant radio gateway was **audited before it was allowed to send**.
> - **Public documentation:** a privacy review led to anonymised commit identity, stripped image metadata, true PDF redaction, vendor names withheld for personal cloud accounts, and security logic not published.

**Portfolio position:** Management level · OT/BMS cyber security. Related: [HA integration schedule](https://github.com/the-control-cabinet/home-assistant-integration-schedule) (write-access tiers) · [Evohome RAMSES-II](https://github.com/the-control-cabinet/evohome-heating-controls-ramses-integration) (transmit audit)

---

## 1. Principles (the OT mapping)

| OT / BMS principle | Applied here |
|---|---|
| **Minimise exposure** | No router port-forwards; remote access through an encrypted relay only; local-first integrations |
| **Least privilege** | Integrations read-only unless there's a defined need to command. Write access tiered (safety, plant, security, comfort) |
| **Defence in depth** | Field systems work stand-alone (heating, fire/CO, security) and keep working if the head-end is compromised or down |
| **Secure communications** | Encrypted ESPHome APIs; MQTT with authentication; encrypted remote relay |
| **Credential management** | Secrets files kept outside published configs; unique credentials per service |
| **Know what talks to what** | An integration schedule of every system, protocol, path and direction |
| **Verify transmitters** | A plant RF gateway was audited (what it sends, to whom) before transmit was enabled, and re-audited after changes |
| **Supply chain / updates** | Maintained integrations preferred; firmware and add-ons kept current; changes re-audited |

## 2. Checklist

### Network and remote access
- [x] No inbound port-forwards to the head-end; UPnP not used for it.
- [x] Remote access via an encrypted cloud relay only.

### Devices
- [x] ESPHome native API **encryption** on every board.
- [x] Fallback hotspots with strong passwords. **Generic SSIDs**, so they don't identify the location of the device.
- [x] Static DHCP reservations for locally integrated LAN devices (stability, and an audit of what's on the network).

### Credentials
- [x] All credentials in `secrets.yaml` (HA) and the ESPHome secrets file. **Never committed.**

### Command authority
- [x] Write access tiered: **safety** (alarm sounder: detached, auto-off), **plant** (heating: audited transmit), **security** (automation-only, details withheld), **comfort**.
- [x] A plant radio gateway allowed to transmit only **after a transmit audit** (only reads and temporary setpoints were sent); re-audited after any change.
- [x] Zigbee network key and device keys never published.

### Monitoring
- [x] Alerts when critical interfaces go offline (e.g. the fire/CO interface).

### Publishing (privacy) hygiene
- [x] Commit identity uses the platform's **no-reply address**. History rewritten (repos recreated) after a personal address was found in old commits.
- [x] **Image metadata (EXIF/GPS)** checked and stripped.
- [x] **PDF redaction removes the text itself** (not just a box over it); metadata cleared; internal streams checked.
- [x] **Vendor names withheld** for cloud services tied to personal accounts (reduces targeted phishing).
- [x] **Security-system logic not published** (alarm, locks, cameras, entrances).
- [x] No IPs, MACs, device IDs (masked), Wi-Fi names, keys, or personal or location names.
- [x] A periodic **live audit** of all repos (history, content, images, links).

## 3. The publishing review: what was found and fixed

| Finding | Risk | Fix |
|---|---|---|
| Personal email in every commit's metadata | Cross-links the code identity to a real person; phishing and credential-stuffing target | Platform email privacy on; repos recreated for clean history |
| Personal email inside diagram PDFs | Same | True redaction (text removed), metadata cleared |
| A list of personal cloud vendors | A targeting kit when combined with an email | Named by function, not vendor |
| Security automations described in detail | Physical-security intelligence | Described at category level only |
| Fallback Wi-Fi names naming rooms | Links a physical location to the public repos | Made secrets, with generic names |

## 4. Continuous improvement
Hardening is reviewed periodically against these principles. **Open items are tracked privately, not published:** a public list of controls not yet in place would be a map for an attacker. That applies to this repo and to every repo in the portfolio.

## 5. Skills demonstrated

| Skill | Evidence |
|---|---|
| OT security principles | Exposure minimisation, least privilege, defence in depth |
| Command-authority control | Risk-tiered write access; transmit audit before enabling |
| Credential and secrets management | Separation, 2FA, rotation |
| Privacy engineering | Commit identity, EXIF, PDF redaction, vendor anonymisation |
| Audit discipline | Periodic live review of published material |

📺 [The Control Cabinet on YouTube](https://www.youtube.com/channel/UC5Cupmz7vlfcodpCX7k8iuQ)

*Built and documented by James · part of [The Control Cabinet BMS portfolio](https://github.com/the-control-cabinet). MIT Licence.*
