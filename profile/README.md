<div align="center">

# R*mble

**Organisation GitHub · [Ramble-cstjean](https://github.com/Ramble-cstjean)**

Application de clavardage de bureau pour discuter avec vos amis et vos partenaires de jeu — **en développement actif**.

<br />

[![Orchestration · Docker · start-all](https://img.shields.io/badge/Documentation_%26_d%C3%A9marrage-A26__5A6__04--Rambl-6366f1?style=for-the-badge&logo=docker&logoColor=white)](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl)

<br />

![Electron](https://img.shields.io/badge/Electron-191970?style=flat-square&logo=electron&logoColor=white)
![React](https://img.shields.io/badge/React-20232a?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=flat-square&logo=laravel&logoColor=white)
![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat-square&logo=mariadb&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

</div>

---

## Démarrer ici

Toute la stack (Docker Compose, variables d'environnement, scripts `start-all` / `test-stack`, schéma d'architecture) est documentée dans le dépôt d'**orchestration** :

**→ [A26_5A6_04-Rambl](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl)** — point d'entrée du projet Rambl.

Les dépôts ci-dessous contiennent le code de chaque service ; seul `A26_5A6_04-Rambl` les assemble pour le développement local.

---

## Objectif

Offrir une application **nouvelle et fiable** pour rester connecté pendant vos sessions de jeu en ligne : messages, salons, présence et temps réel, avec une architecture multiservice claire (API, authentification, base de données, bus d'événements).

---

## Stack · aperçu

| Domaine | Technologies |
| :-- | :-- |
| **Client desktop** | Electron, React 18, TypeScript, Vite |
| **Client mobile** | React Native (Expo) — dépôt séparé, hors orchestration Docker actuelle |
| **API REST** | Laravel (PHP), validation et lecture DB, publication des écritures sur Redis |
| **Authentification** | Rust — service dédié ; l'API appelle `POST /auth/v1/authorize` à chaque requête |
| **Base de données** | MariaDB — source de vérité (comptes, salons, messages) |
| **Temps réel** | Redis (Pub/Sub) + EventBus Node.js/TypeScript (`ws` + `db-writer`) |
| **Panneau admin** | React 19, Vite, Tailwind — rôle `admin` requis |
| **Orchestration** | Docker Compose et scripts `.sh` / `.ps1` dans [A26_5A6_04-Rambl](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl) |

Pour le détail des flux (écriture 202 → EventBus → DB + WebSocket), des ports et des prérequis, voir le README d'orchestration.

---

## Dépôts, tags et artefacts

Versions compatibles de la remise du 11 novembre 2026 (pré-versions). Chaque tag pointe sur la branche `main` de son dépôt : `start-all --source main` démarre exactement cet ensemble (`--source release` l'ignore, car il ne retient que les tags stables).

| Rôle | Dépôt | Tag | Artefact |
| :-- | :-- | :-- | :-- |
| **Orchestration** *(commencer ici)* | [A26_5A6_04-Rambl](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl) | [`v.2.0.0-beta.1`](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl/tree/v.2.0.0-beta.1) | Scripts `start-all` / `stop-all` / `test-stack` (`.sh` et `.ps1`) |
| Application desktop | [A26_5A6_04-Ramble-frontend](https://github.com/Ramble-cstjean/A26_5A6_04-Ramble-frontend) | [`latest`](https://github.com/Ramble-cstjean/A26_5A6_04-Ramble-frontend/tree/latest) (v2.1.0) | [Release `latest`](https://github.com/Ramble-cstjean/A26_5A6_04-Ramble-frontend/releases/tag/latest) : `Rambl-Windows-Setup.exe`, `Rambl.dmg`, `Rambl.AppImage` (non signés) |
| API REST | [A26_5A6_04-Rambl-api-rest](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-api-rest) | [`v.2.0.0-beta.1`](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-api-rest/tree/v.2.0.0-beta.1) | Image Docker construite par `start-all` |
| Service d'authentification | [A26_5A6_04-Rambl-service-authentification](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-service-authentification) | [`v3.0.0-beta.1`](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-service-authentification/tree/v3.0.0-beta.1) | Image Docker construite par `start-all` |
| Schéma et migrations (MariaDB) | [A26_5A6_04-Rambl-BD](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-BD) | [`v1.0.0-beta.1`](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-BD/tree/v1.0.0-beta.1) | Images Docker construites par `start-all` (MariaDB, réplique, seeder, `backup-runner`) |
| Bus d'événements (WebSocket + écriture DB) | [A26_5A6_04-Rambl-EventBus](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-EventBus) | [`v2.0.0-beta.1`](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-EventBus/tree/v2.0.0-beta.1) | Images Docker construites par `start-all` (`ws`, `db-writer`) |
| Panneau d'administration | [A26_5A6_04-Rambl-panneau-administateur](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-panneau-administateur) | [`v1.0.0-beta.1`](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-panneau-administateur/tree/v1.0.0-beta.1) | Lancé par `start-all` (`http://localhost:5174`) + conteneur `services-probe` |
| Application mobile | [A26_5A6_04-Rambl-React-Native](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-React-Native) | [`v2.0.0`](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-React-Native/tree/v2.0.0) | Aucun APK publié : build Expo local (voir le README du dépôt) |

---

## Accès

- **Dépôts** : privés. Il faut être membre de l'organisation Ramble-cstjean, avec une clé SSH ajoutée à GitHub (`start-all` clone en `git@github.com:...`).
- **Stack locale** : après `start-all`, le desktop s'ouvre seul ; panneau admin sur `http://localhost:5174`, API `:8000`, authentification `:8081`, WebSocket `:4000`.
- **Compte administrateur** : créé par le seeder à partir de `ADMIN_EMAIL` / `ADMIN_PASSWORD` du `.env`. Les identifiants de démonstration sont transmis séparément, jamais dans ce dépôt public.
- **Infrastructure de dev distante** : accès restreint par IP (liste blanche) ; voir [le guide de déploiement](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl/blob/develop/docs/deploiement-dev.md) du dépôt d'orchestration.

<details>
<summary><strong>Prévu · pas encore développé</strong></summary>

| Rôle | Dépôt |
| :-- | :-- |
| Routeur Nginx | [A26_5A6_04-Rambl-Router-Nginx](https://github.com/Ramble-cstjean/A26_5A6_04-Rambl-Router-Nginx) |

</details>

---

## Équipe · CST Jean

| | GitHub |
| :-- | :-- |
| Xavier Boudreau | [@Xavier-Boudreau](https://github.com/Xavier-Boudreau) |
| Galilée Wandji | [@GalileeWandji11](https://github.com/GalileeWandji11) |
| Nicolas Tremblay | [@ChimiChanga75](https://github.com/ChimiChanga75) |
| Henri Blanchard | [@HenriBlanchard](https://github.com/HenriBlanchard) |
| Christin Soulières | [@sinistershadow18](https://github.com/sinistershadow18) |
| Vincent Hottin | [@v1nny31](https://github.com/v1nny31) |
| Yacine Idir | [@YacineIdir](https://github.com/YacineIdir) |

---

<div align="center">

*Rambl · projet A26_5A6_04 · [Ramble-cstjean](https://github.com/Ramble-cstjean)*

</div>
