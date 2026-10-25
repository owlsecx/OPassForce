# 🦉 OPassForce

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux-0a0c10?style=flat-square"/>
  <img src="https://img.shields.io/badge/Category-OAttack%20/%20Offensive-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-1.0-cyan?style=flat-square"/>
</p>

> **OPassForce** — Defensive Auth Audit Suite ║

---

> ⚠️ **AUTHORISED USE ONLY** — Use only on systems you own or have explicit written permission to test. Unauthorised use is illegal.

---

## 📌 Overview

OPassForce is a defensive authentication-flow audit suite for web applications. It analyses login flows for CSRF, session and redirect handling, inspects cookies, and detects rate-limiting and WAF hints from response heuristics. It performs no brute-force attacks and defaults to a safe dry-run mode.

---

## ✨ Features

- Audits authentication flows for CSRF, session and redirect weaknesses
- Detects rate-limiting and WAF behaviour from response heuristics
- Inspects cookies and HTTP response characteristics
- Operates in a dry-run mode by default, with no live POST until explicitly enabled
- Optional confirmation gate before testing remote targets
- Explicitly avoids brute-force techniques

---

## ⚙️ Requirements

- **Linux**
- **No Python installation needed** — runs as a standalone executable

---

## 🚀 Usage

```bash
./OPassForce
./OPassForce --no-dry-run
./OPassForce --allow-remote
./OPassForce --help
```

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 300+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

MIT License — © Khaled S. Haddad

*Tools are distributed as pre-built executables. Source code is proprietary.*
