# PengWin — Linux Server Control Panel (Showcase)

Fast, reliable, and student-friendly web GUI for configuring **DHCP, DNS, Samba, Apache**, and more — without hand-editing config files.

> **Showcase repo:** This is a documentation-only public summary of our capstone project.  
> It intentionally excludes real configs, sudoers entries, and internal scripts.

---

## 🐧What is PengWin?🐧

**PengWin** is a Flask-based web control panel that lets IT students and junior sysadmins set up common Linux services through **clean, guided forms**.  
No manual `dhcpd.conf` editing, no scary `named.conf` typos, no guessing which service to restart — PengWin generates configs, validates input, applies changes, and shows service status from one dashboard.

**Value proposition (from our team docs):**

> “PengWin empowers IT students, junior sysadmins, and lab users with a fast, reliable, and user-friendly way to configure core Linux services. By eliminating the frustration of command-line setup, we make Linux server management simpler, smarter, and more accessible — all from one intuitive web interface.”

---

## 🎯 Who is it for?

- **IT students / junior sysadmins** learning Linux services
- **Instructors & training labs** who want repeatable demos
- **Small teams** needing quick, safe service setup in test environments

---

## ✨ Features

- **DHCP (isc-dhcp-server)** — define subnets, ranges, routers, DNS
- **DNS (BIND / named)** — zones, A records, validation
- **Samba** — simple file share creation (Linux/Windows tested)
- **Apache (virtual hosts)** — basic vhost generation (showcase scope)
- **Dashboard** — service status + start/stop (systemd)
- **Backups** — save current config before overwrite
- **Input validation** — reduce broken configs and crash loops
- **Audit trail (design)** — log what changed and when

> Modules also explored in later sprints: **Firewall, NTP, FTP, VNC, Hostname change, Auth/Login** (see roadmap).

---

## 🧱 Architecture (High-level)

Browser (Bootstrap UI)

|

Flask (app.py routing)

│

├─ modules/dhcp.py ──> generate + validate dhcpd.conf

├─ modules/dns.py ──> named.conf / zones

├─ modules/samba.py ──> smb.conf shares

├─ modules/apache.py──> vhost files

│

└─ safe subprocess wrappers (systemd start/stop/status)

↑

limited sudoers (NOPASSWD) for specific commands only


- Backend uses **config templates + input validation** to write clean files.
- **Systemd** handles service lifecycle; we display status on the dashboard.
- **Sudoers** is restricted to the minimum commands (design principle, not included here).

---

## 🖼️ Screenshots

- Dashboard — `![Dashboard](screenshots/dashboard.png)`
- DHCP Form — `![DHCP](screenshots/dhcp.png)`
- DNS Form — `![DNS](screenshots/dns.png)`
- Samba Form — `![Samba](screenshots/samba.png)`

---

## 🧪 What we built (by sprints)

**Sprint 1 (June 3–23)** — *Foundation & Core Services*  
- Flask app scaffold, **DHCP & DNS** forms and generators  
- Subprocess + sudo approach researched and tested  
- Config backup and validation patterns drafted  
- GitHub Projects board + team workflow

**Sprint 2 (June 24–July 14)** — *Expand & Stabilize*  
- **Samba** functionality completed (Linux confirmed; Windows integration fixed)  
- Debugged DHCP/DNS issues and improved reliability  
- Dashboard service status in progress  
- Scoped out Apache & logging (moved)

**Sprint 3 (July 15–Aug 8)** — *Polish & Extras*  
- UI redesign (clean + simple)  
- Added **Firewall, NTP, FTP, VNC, Hostname** modules (showcase scope)  
- Merged separate Ubuntu/CentOS versions into unified structure  
- Modularized code: `app.py` routes ➜ per-service modules

> Sources: Sprint reports and project plan you provided.

---

## 🧩 Tech Stack

- **Python / Flask** — web routing & forms
- **Bootstrap 5** — layout and components
- **Bash + systemd** — safe service control
- **Linux services** — isc-dhcp-server, bind/named, smbd/nmbd, apache2/httpd
- **GitHub Projects** — agile/kanban, issues, sprints

---

## 🔐 Security Notes (Showcase)

- No real **sudoers** content is included. In production, restrict to explicit, minimal commands.  
- Validate *all* user input before writing files.  
- Always **backup** current configs before overwriting.  
- Prefer **config preview** + “Apply” confirmation.

---

## 🗺️ Roadmap

- ✅ DHCP, DNS, Samba basics
- ✅ Apache vhosts (showcase scope)
- 🔜 Stronger input validation + error messages
- 🔜 Live service health checks on dashboard
- 🔜 Authentication / login for panel access
- 🔜 Full audit logging (append-only)
- 🔜 Dockerized dev environment for quick spin-up

---

## 🧠 Lessons Learned (from team notes)

- Foundation first: functionality before styling saved us from rework.
- Validations + config backups are essential — one bad file can brick a service.
- Sudoers must be precise; avoid broad permissions.
- Merging parallel versions (Ubuntu/CentOS) requires early alignment.
- Git hygiene matters: commit stable milestones before UI changes.

---

## 🧑‍🤝‍🧑 Team

**Group 5** — Aira Therens, Amrit Kaur Dhiman, Angelo Verzosa, Carl Louis Canillo,  
Chan Quyen Khuu, Yug Sanjay Kinkhabwala

---

## 📚 Sources for this README

All content here is drawn from your **project plan, sprint reports, value proposition, backlog, and technology notes** you shared above (no external sources, and no fabricated details). This is a showcase summary of your actual work — cleaned up for public viewing.

---

## 📄 License
Documentation © Group 5 (SAIT).
