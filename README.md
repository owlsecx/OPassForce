# 🦉 OPassForce

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux%20%2F%20Windows-informational?style=flat-square&logo=linux&logoColor=white&color=0a0c10"/>
  <img src="https://img.shields.io/badge/Category-OWeb%20%2F%20Auth%20Analysis-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Interface-GUI-magenta?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-1.0-cyan?style=flat-square"/>
</p>

> **OPassForce** is a defensive authentication audit suite with a dark-themed GUI. It inspects login form behaviour, CSRF/session handling, redirect chains, and rate-limit / WAF presence — without performing any brute-force attacks.

---

> ⚠️ **AUTHORISED USE ONLY** — This tool does **not** perform brute-force attacks. Use only on systems you own or have **explicit written permission** to test.

---

## 📌 Overview

OPassForce sends a minimal number of controlled HTTP requests to audit how a login endpoint behaves — analysing response bodies, status codes, cookies, hidden fields, redirect destinations, and protection headers — and presents all findings in a live results table and colour-coded audit log.

---

## 🖥️ Interface

The GUI is split into two panels:

**Left Panel — Configuration**

| Field | Description |
|-------|-------------|
| **Profile** | Select audit mode (Sniper / Cluster Bomb / PitchFork) |
| **Login POST URL** | Full URL the login form submits to |
| **POST data template** | Form body with `^USER^` and `^PASS^` placeholders — e.g. `username=^USER^&password=^PASS^` |
| **Username** | Single username to test (or login page URL for Cluster Bomb) |
| **Password / keyword** | Single password or a success keyword to detect in the response |
| **▶ START AUDIT** | Begin the selected profile |
| **■ STOP** | Abort the current audit |

**Right Panel — Results**

| Section | Description |
|---------|-------------|
| **Audit Results table** | Check name · Result · HTTP status · Details — colour-coded green / amber / red |
| **Audit Log** | Scrollable real-time log with tagged output |

---

## 🎯 Profiles

### Sniper — Single Login Test
Submits one `username:password` pair against the target URL and analyses the full HTTP response chain:
- Fetches the login page and extracts any hidden / CSRF fields before submitting
- Injects hidden fields alongside credentials in the POST body
- Analyses response for failure markers (`invalid`, `incorrect`, `authentication failed`, …) and success markers (`dashboard`, `logout`, `welcome`, …)
- Follows redirect chains and fingerprints the destination page
- Checks session cookies set after the request
- Returns verdict: `LIKELY_SUCCESS` / `LIKELY_FAILED` / `UNCERTAIN`

### Cluster Bomb — Auth Flow Audit
No password guessing. Audits the full authentication flow:
- Fetches the login page (GET URL goes in the Username field)
- Extracts all hidden input fields (CSRF tokens, nonces, etc.)
- Sends a dummy-credential probe POST with extracted fields merged in
- Inspects cookies, redirect behaviour, and response delta vs baseline
- Runs an inline PitchFork check on the POST endpoint

### PitchFork — Rate-Limit & WAF Detection
Sends minimal safe GET requests to the target URL and inspects protection signals:
- HTTP `429` — rate limiting active
- HTTP `401` / `403` — WAF or access block
- `cf-ray` header — Cloudflare detected
- `x-rate-limit-*` headers — rate-limit headers present
- Cloudflare `Server` header fingerprint

---

## 🔍 Response Analysis

Every HTTP response is analysed against:

| Signal | Meaning |
|--------|---------|
| Failure markers in body | `invalid`, `incorrect`, `wrong password`, `unauthorized`, … |
| Success markers in body | `dashboard`, `logout`, `my account`, `welcome`, … |
| Custom keyword match | User-supplied keyword found in response body |
| HTTP status code | `302` redirect, `429` rate limit, `401/403` blocked |
| Response length delta | Significant size difference from baseline → behaviour change |
| Set-Cookie header | Session cookie issued — possible auth signal |

---

## 📊 Result Colours

| Colour | Meaning |
|--------|---------|
| 🟢 Green | Check passed / success signal detected |
| 🟡 Amber | Warning — uncertain result or missing field |
| 🔴 Red | Failure — error, blocked, or rate limited |

---

## ⚙️ Requirements

- **Linux or Windows**
- **No Python installation needed** — runs as a standalone executable

---

## 🚀 Usage

```bash
./OPassForce
```

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 300+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

MIT License — © Khaled S. Haddad

*Tools are distributed as pre-built executables. Source code is proprietary.*
