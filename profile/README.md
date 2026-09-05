<div align="center">

# Quant Studio SARL

### Groupe technologique — Cotonou, Bénin 🇧🇯

**Édition de logiciels · SaaS académique · Formation data & IA**

<br>

![Bénin](https://img.shields.io/badge/Cotonou-B%C3%A9nin-008751?style=for-the-badge&labelColor=E8112D)
![OHADA](https://img.shields.io/badge/March%C3%A9-OHADA-FCD116?style=for-the-badge&labelColor=333)
![Odoo](https://img.shields.io/badge/Odoo-19-714B67?style=for-the-badge&logo=odoo&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-16-000000?style=for-the-badge&logo=next.js&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)

</div>

---

<div align="center">

> **Bienvenue dans l'organisation.** 👋
> Cette page répond à trois questions : **ce qu'on fait**, **où est quoi**, et **qui fait quoi**.
> Nouveau venu ? File directement à **[Par où commencer ↓](#-par-o%C3%B9-commencer-nouveau-venu)**

</div>

---

## 🧭 Ce qu'on fait

Quant Studio SARL conçoit et édite des logiciels pour le marché africain. Le groupe s'organise en **trois pôles** :

<table>
<tr>
<td width="33%" valign="top">

### 🛠️ Teklane
**Ingénierie logicielle**

Édition de l'ERP, outils métier, veille automatisée et sites. Le pôle produits & régie.

</td>
<td width="33%" valign="top">

### 📚 Thesigenix
**SaaS académique**

Accompagnement des étudiants et chercheurs : store de sujets, encadrement méthodologique.

</td>
<td width="33%" valign="top">

### 🎓 Quanty Mind
**Formation**

Formation professionnelle : analyse de données, mathématiques et IA.

</td>
</tr>
</table>

---

## 🗂️ Où est quoi

> **Statut** — 🟢 `prod` : en production · 🟡 `dev` : développement actif · 🔵 `interne` : outil interne

### 🛠️ Teklane — ingénierie logicielle

| Repo | Description | Stack | Statut |
|:---|:---|:---|:---:|
| [**erp**](https://github.com/QuantStudioAfrik/erp) | **Quant Studio Suite** — suite d'apps Odoo 19 propriétaires : compta, paie, contrats (CLM), courrier, signature. Localisations OHADA (17 pays) + Bénin (CNSS/IPRES/IRPP, DGI). Licence QSEL-1.0. | `Odoo 19` `Python` `Docker` | 🟡 |
| [**scanner**](https://github.com/QuantStudioAfrik/scanner) | **DAO Scanner** — robot de veille d'appels d'offres : ratisse les portails de marchés publics, juge chaque AO via LLM (Ollama) et pousse les projets d'ingénierie logicielle dans Odoo (`crm.ao`). | `Python` `Ollama` `Odoo` | 🔵 |
| [**scrapping-article**](https://github.com/QuantStudioAfrik/scrapping-article) | Veille presse full-stack : scraping multi-moteurs (Cheerio/Playwright/Puppeteer/Selenium), suivi de mots-clés, alertes, dashboard + API REST, exports CSV/XLSX. | `Node.js` `REST` | 🟡 |
| [**vitrine-quant-studio**](https://github.com/QuantStudioAfrik/vitrine-quant-studio) | Site vitrine du groupe. | `Next.js 16` `Tailwind v4` | 🟡 |
| [**open-design**](https://github.com/QuantStudioAfrik/open-design) | Alternative open-source à Claude Design : agent de design + génération d'images. | `Node` `Desktop` | 🟡 |
| [**OpenMontage**](https://github.com/QuantStudioAfrik/OpenMontage) | Système agentique open-source de production vidéo (pipeline `backlot`). | `Python` | 🟡 |

### 📚 Thesigenix — SaaS académique

| Repo | Description | Stack | Statut |
|:---|:---|:---|:---:|
| [**thesigenix**](https://github.com/QuantStudioAfrik/thesigenix) | Plateforme d'accompagnement des étudiants et chercheurs : store de sujets structurés (problématique, revue de littérature, méthodologie), encadrement, gestion multi-rôles (7 rôles). | `Next.js 16` `TypeScript` `MongoDB` `Docker` | 🟡 |

### 🎓 Quanty Mind — formation

<!-- Aucun repo de code à ce jour ; supports de formation hors GitHub. Ajouter ici les repos éventuels (notebooks, générateurs d'exercices). -->
_Supports de formation gérés hors GitHub pour l'instant. Les repos éventuels (notebooks, générateurs d'exercices) viendront ici._

### 🧩 Infra & outils déployés

Outils open-source tiers exploités en production. On ne les édite pas, on les déploie/configure.

| Outil | Rôle chez nous |
|:---|:---|
| [**docuseal**](https://github.com/QuantStudioAfrik/docuseal) | Signature électronique de documents (alternative DocuSign) — branché au module Signature de la Suite. |

---

## 👥 Qui fait quoi

<table>
<tr>
<td align="center" width="33%">

### David Akpovi
`Fondateur`

Direction · vision produit

</td>
<td align="center" width="33%">

### Balbine MAMADOU
`Tech Lead`

Architecture · revue technique

</td>
<td align="center" width="33%">

### Marthely
`Développeur`

Développement produit

</td>
</tr>
</table>

**Qui contacter pour quoi**

- **Question technique / architecture / revue** → **Balbine MAMADOU** (Tech Lead)
- **Développement produit au quotidien** → **Marthely**
- **Direction / vision / priorités** → **David Akpovi**

<!-- Compléter : référents par repo, autres membres de l'équipe, contacts (email/Slack). -->

---

## 🚀 Par où commencer (nouveau venu)

1. **Accès** — Demande à ton référent l'accès à l'org GitHub `QuantStudioAfrik` et au gestionnaire de secrets (**Passbolt**). Aucun secret ne se partage en clair.
2. **Clone le repo** sur lequel tu travailles (voir [Où est quoi ↑](#%EF%B8%8F-o%C3%B9-est-quoi)). Chaque repo a son `README` avec le lancement local.
   - **ERP** → `docker compose up -d` puis backoffice sur `http://localhost:8082`
   - **Front** (thesigenix, vitrines) → `pnpm install && pnpm dev`
3. **Lis le `README` et le `CLAUDE.md`** du repo avant de coder : ils portent les conventions locales.
4. **Suis le workflow de dev** ci-dessous — *pas de code sans design approuvé.*

---

## ⚙️ Nos conventions

Le développement suit le framework interne **super-dev** (plugin Claude Code) :

| Étape | Commande | Quand |
|:---|:---|:---|
| Dérouler une feature de bout en bout | `/build` | Toute nouvelle fonctionnalité |
| Vérifier avant commit | `/verify` | Avant chaque commit |
| Passe d'authenticité (style) | `/ghostwrite` | Avant de livrer |
| Revue de sécurité | `/security` | Sur toute surface sensible |
| Hors-scope | `/backlog` | Idée qui sort du périmètre |

> 🔒 **Règle d'or : jamais de code sans design approuvé.**

- **Licences** — le code produit est sous **QSEL-1.0** (Quant Studio Edition License) sauf mention contraire ; voir le `LICENSE` de chaque repo.
- **Secrets** — jamais dans le code ni dans un README. **Passbolt** uniquement.

---

## 🔗 Liens utiles

<!-- À compléter : sites en prod, docs internes, drive, board projet. -->

- 🌐 Site du groupe — _(à préciser)_
- 📚 Thesigenix — _(à préciser)_
- 📁 Documentation interne / drive — _(à préciser)_

---

<div align="center">
<sub>⚡ <b>Quant Studio SARL</b> · Cotonou, Bénin · page d'onboarding interne</sub>
</div>
