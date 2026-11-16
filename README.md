# DGP | Damions Game Panel

**DGP (Damions Game Panel)** is a lightweight, self-hosted web management panel built with **Node.js / TypeScript (Fastify)**, **Vue 3 (Vite)**, and **SQLite (WAL + FTS5)** for managing dedicated game servers on Ubuntu Linux [source: 0.6.33, 0.6.35].

---

## Core Architecture & Features

- **Multi-Game Server Management:**
  - Dedicated instance lifecycle management, shared-file provisioning, and systemd `cGroup v2` resource isolation (`AllowedCPUs`, `MemoryMax`) for **ARK: Survival Ascended**, **ARK: Survival Evolved**, and **Minecraft** (Vanilla, Paper, Purpur, Fabric, Forge) [source: 0.6.35, 0.6.39, 0.6.40].
- **CurseForge & Modrinth Mod Manager:**
  - Server-side mod lookup by name or Mod ID, visual load-order sorting, and automatic startup parameter synchronization (`-mods=...`) [source: 0.6.40].
  - Local SQLite metadata caching (`mod_catalog`) to minimize external API calls [source: 0.6.37].
  - *No mod files are mirrored, hosted, or redistributed by the panel; all game mods are fetched directly via official game server flags (`-automanagedmods`) or official client mod browsers.*
- **Real-Time Telemetry & Historical Metrics:**
  - 5-second `cGroup v2` resource collector (CPU, RAM, Disk I/O, Network) backed by SQLite WAL with automatic downsampling and annual archive exports [source: 0.6.38].
- **RCON Console & FTS5 Event Log Search:**
  - WebSocket live console, native TCP RCON integration, player list & whitelist synchronization, and full-text searchable event archives (`SQLite FTS5`) [source: 0.6.38, 0.6.40].
- **Backup Vault & Cross-Server Clustering:**
  - `zstd`-compressed world snapshots with SHA-256 checksums, 1-click rollback, scheduled tasks, and cross-server cluster management [source: 0.6.38, 0.6.40].
- **Security & Configuration Integrity:**
  - Role-Based Access Control (RBAC), Nginx reverse proxy with TLS, and immutable configuration file protection (`chattr +i`) for `GameUserSettings.ini` and `Game.ini` [source: 0.6.35, 0.6.37, 0.6.41].

---

## Tech Stack

- **Backend:** Node.js 22 LTS, TypeScript, Fastify, Better-SQLite3 (WAL + FTS5) [source: 0.6.35, 0.6.36]
- **Frontend:** Vue 3, Vite, Pinia [source: 0.6.35]
- **Infrastructure:** Ubuntu Linux, systemd `cGroup v2`, Nginx, UFW, RCON [source: 0.6.35, 0.6.40, 0.6.41]

---

## Security & API Key Policy

- External API keys (such as the **CurseForge Core API** key) are stored exclusively on the backend server inside an access-restricted SQLite database and are never exposed to browser clients or committed to version control.
