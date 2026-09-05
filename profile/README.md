# 👋 Bienvenue dans l'équipe

Salut, et bienvenue. Si tu lis ça, c'est que tu viens d'être recruté·e, donc que quelqu'un ici t'a fait assez confiance pour te donner un siège sur notre GitHub. Félicitations, et merci d'embarquer. On est vraiment contents de t'avoir (et pas seulement parce qu'on avait besoin de bras).

Ce dépôt existe pour une raison un peu égoïste : que **tu n'aies jamais à déranger quelqu'un sur le chat pour comprendre comment on fonctionne**. Où vivent les serveurs, comment s'y connecter, qui a écrit quoi, et ce qu'on refusera gentiment en revue : tout est ici.

Garde cet esprit vivant. Le jour où tu quittes l'équipe, la personne suivante doit pouvoir lire ce même README, sauter la cérémonie du « café d'intro avec le·la senior », et livrer du code dès sa première matinée. Si tu découvres un truc qui n'est pas documenté ici, la règle tient en trois mots : **documente-le avant de l'oublier**. Le toi du futur t'offrira une bière pour ça.

Lis à ton rythme, dans l'ordre que tu veux. La table des matières est juste en dessous. Et non, il n'y a pas d'examen à la fin.

---

## 🗺️ Table des matières

| # | Section | En un mot |
|:-:|---|---|
| 1 | [Se connecter à un serveur](#1-se-connecter-à-un-serveur) | Ta clé, tes accès |
| 2 | [DNS & noms de domaine](#2-dns--noms-de-domaine) | Où pointent les flèches |
| 3 | [La stack](#3-la-stack) | Ce avec quoi on code |
| 4 | [Comment on bosse](#4-comment-on-bosse) | À faire / à éviter |
| 5 | [Workflow Git](#5-workflow-git) | Branche, PR, merge, répète |
| 6 | [Secrets & accès](#6-secrets--accès) | Le coffre, et pourquoi git n'en est pas un |
| 7 | [Projets & dépôts](#7-projets--dépôts) | La carte du royaume |
| 8 | [Qui est qui](#8-qui-est-qui) | À qui parler avant de paniquer |

> [!TIP]
> Tu n'as que 15 minutes aujourd'hui ? Envoie ta clé SSH ([section 1](#1-se-connecter-à-un-serveur)), lis [comment on bosse](#4-comment-on-bosse), puis clone ton projet ([section 7](#7-projets--dépôts)) et essaie de le lancer en local. Le reste peut dormir jusqu'à demain.

---

## 1. Se connecter à un serveur

> [!IMPORTANT]
> **En bref :** clé SSH uniquement. Pas de root, pas de mot de passe. Tu envoies ta clé **publique** au référent, jamais la privée.

### Les règles de base (celles qu'on ne négocie pas)

- **Le login root par SSH est désactivé.** Ne le demande pas, ne l'active pas « juste cinq minutes ». Les intrusions **adorent** les « juste cinq minutes ».
- **Le mot de passe est désactivé.** Oui, même le tien qui est très fort. La seule porte d'entrée, c'est une clé.
- **Pas de comptes partagés.** Tu as ton propre utilisateur Unix, avec `sudo` là où c'est justifié. Ce que tu casses porte ton nom (motivant, non ?).

### Obtenir l'accès, pas à pas

**1. Génère ta paire de clés** sur ta machine. On utilise Ed25519 :

```bash
ssh-keygen -t ed25519 -C "prenom@quant-studio"
```

Mets une vraie passphrase. Une clé sans passphrase, c'est une clé de maison scotchée à la porte d'entrée.

**2. Envoie la clé publique** au référent. C'est le fichier qui finit en `.pub` (`~/.ssh/id_ed25519.pub`), sur un canal où il peut vérifier que c'est bien toi.

> [!WARNING]
> **N'envoie JAMAIS la clé privée.** Ni sur le chat, ni par mail, ni « juste à toi-même dans un brouillon ». Si ça t'arrive : régénère une paire, point. Aucune honte, juste une rotation.

**3. Le référent ajoute ta clé** dans `~/.ssh/authorized_keys` et te renvoie ton nom d'utilisateur + le hostname.

**4. Connecte-toi :**

```bash
ssh <ton-utilisateur>@<hostname>
```

### Nos serveurs

On tourne sur **deux serveurs** : un chez **Hetzner**, un chez **Infomaniak**.

<!-- À COMPLÉTER : hostname, OS, rôle et services de chaque serveur. Garder le même format d'une colonne à l'autre. -->

| Élément | Hetzner | Infomaniak |
|---|---|---|
| Hostname | _à préciser_ | _à préciser_ |
| OS | _à préciser_ | _à préciser_ |
| Rôle principal | _à préciser_ | _à préciser_ |
| Services hébergés | _à préciser_ | _à préciser_ |

---

## 2. DNS & noms de domaine

> [!IMPORTANT]
> **En bref :** on pose le DNS **avant** la conf nginx. Certbot a besoin que le nom résolve déjà, il n'est pas devin.

<!-- À COMPLÉTER : registrar, fournisseur DNS, procédure d'ajout de sous-domaine. -->

- **Registrar / DNS :** _à préciser_
- **Reverse proxy / TLS :** Nginx + Certbot (Let's Encrypt) devant les conteneurs.

Deux règles qui font gagner des heures :

- **Mail** (`MX`, SPF, DKIM, DMARC) : réglages à part, jamais derrière un proxy HTTP.
- **Tu supprimes un service ? Supprime son enregistrement DNS.** Un record fantôme qui pointe vers un serveur qu'on ne contrôle plus, c'est le tapis rouge d'une prise de contrôle de sous-domaine.

---

## 3. La stack

On n'est pas l'équipe « on réécrit tout dans le framework de la semaine ». On choisit un petit jeu d'outils, et on devient bons dessus.

| Catégorie | Ce qu'on utilise |
|---|---|
| **Langages** | Python · TypeScript |
| **Frameworks & runtimes** | Odoo 19 · Next.js · Express · Node.js |
| **Bases de données** | PostgreSQL · MongoDB |
| **Conteneurs & proxy** | Docker Compose · Nginx · Certbot |
| **Mail** | Postfix (SMTP signé DKIM) |

> [!NOTE]
> Envie d'ajouter un nouvel outil ? Ouvre une discussion d'abord. La barre n'est pas « est-ce que c'est cool » (tout est cool le vendredi soir), c'est « est-ce que ça vaut le deuxième outil qu'on devra patcher, monitorer et expliquer à chaque nouveau ».

---

## 4. Comment on bosse

<table>
<tr>
<td width="50%" valign="top">

### ✅ À faire

- **Tout tourne en Docker Compose.** Un projet, un `docker-compose.yml`, et l'hôte reste propre.
- **Les secrets vivent dans Passbolt** (ou un dossier `secrets/` injecté à l'init), jamais dans git.
- **Front en `pnpm`.** Le lockfile fait foi.
- **Modules Odoo sous le préfixe `qs_`**, avec l'en-tête de licence QSEL-1.0 en tête de fichier.
- **Un README par projet** : stack, lancement local, déploiement. Si tu ne sais pas expliquer le démarrage en quelques lignes, c'est ça, le vrai bug.

</td>
<td width="50%" valign="top">

### ❌ À éviter

- **Pas de `Co-Authored-By` dans les commits.** Jamais. C'est notre historique, il reste sobre.
- **Aucune référence externe** (autre éditeur, Enterprise, clean-room…) dans le code, les commentaires ou les messages git.
- **Pas de secret dans git.** Si ça arrive : fais tourner le secret, *puis* nettoie l'historique. Dans cet ordre.
- **Pas de `npm`/`npx` côté front.** On est en `pnpm`, on y tient.
- **Pas de code sans design approuvé.** On cadre, on valide, *ensuite* on code.

</td>
</tr>
</table>

---

## 5. Workflow Git

> [!IMPORTANT]
> **En bref :** on branche, on ouvre une PR, on fait relire, on merge propre. On ne pousse pas en direct sur la branche déployable.

**Branches**
- Une branche par sujet : `feat/<description-courte-kebab>` pour une fonctionnalité, `fix/<description-courte-kebab>` pour un correctif.
- La branche déployable reste toujours dans un état livrable.

**Commits**
- Mode impératif : « Ajoute l'endpoint de matching », pas « Ajouté », pas « des trucs ».
- Un changement logique par commit. Si ton message a besoin du mot « et », c'est probablement deux commits qui font semblant.
- **Pas de `Co-Authored-By`.** (Oui, on le redit. C'est important.)

**Pull requests**
- Une PR se fait **relire** avant le merge. L'auto-merge en solo, c'est pour les gens qui aiment le rollback du dimanche.
- La description dit : ce qui change, pourquoi, comment c'est testé, et le risque éventuel (migration ? downtime ? breaking change ?).
- Une PR de 2000 lignes n'est pas relue, elle est bénie les yeux fermés. Vise petit.

---

## 6. Secrets & accès

- **Passbolt est notre coffre.** Identifiants, clés d'API, accès serveurs : tout y vit. Jamais dans le code, jamais dans un README, jamais sur le chat. Git n'oublie rien, et c'est bien le problème.
- Côté ERP, les secrets de prod (`db`, `smtp`, master password) sont injectés à l'init via l'entrypoint, depuis un dossier `secrets/` **non versionné**.
- Le premier jour, demande à ton référent l'accès à l'org GitHub `QuantStudioAfrik` **et** à Passbolt.
- Chaque service qui parle à un autre a un **compte dédié aux droits minimaux**. Pas de compte admin partagé « pour aller plus vite » : c'est comme ça qu'on va très vite dans le mur.

---

## 7. Projets & dépôts

La carte du royaume. **Chaque projet a son propre README dans son dépôt** : c'est là que tu trouves le setup, le déploiement, les variables d'env et les pièges. Ici, c'est juste l'index, pour savoir ce qui existe et qui pinguer.

> [!NOTE]
> Les **contributeurs** sortent du `git log` de chaque dépôt. Ni une hiérarchie, ni une liste exhaustive. Un nom manquant ou faux ? Ouvre une PR : c'est tout l'intérêt du truc.

### 🛠️ Teklane · ingénierie logicielle

<details open>
<summary><b>Quant Studio Suite (ERP)</b> · le vaisseau amiral 🚩</summary>

<br>

Suite d'apps Odoo 19 propriétaires : compta, paie, contrats (CLM), courrier, signature. Localisations OHADA (17 pays) + Bénin (CNSS / IPRES / IRPP, DGI).

**Dépôt :** [`QuantStudioAfrik/erp`](https://github.com/QuantStudioAfrik/erp)
**Techno :** Odoo 19 · Python · PostgreSQL · Docker Compose · Postfix
**Lancement :** `docker compose up -d` puis le backoffice sur `http://localhost:8082`

</details>

<details>
<summary><b>DAO Scanner</b> · le robot qui lit les appels d'offres à ta place</summary>

<br>

Ratisse les portails de marchés publics, juge chaque AO via un LLM local (Ollama), et ne garde que les projets d'ingénierie logicielle qu'il pousse dans Odoo (`crm.ao`).

**Dépôt :** [`QuantStudioAfrik/scanner`](https://github.com/QuantStudioAfrik/scanner)
**Techno :** Python · Ollama · Odoo

</details>

<details>
<summary><b>Scrapping-Article</b> · la veille presse full-stack</summary>

<br>

Scraping multi-moteurs, suivi de mots-clés, alertes, dashboard + API REST, exports CSV/XLSX.

**Dépôt :** [`QuantStudioAfrik/scrapping-article`](https://github.com/QuantStudioAfrik/scrapping-article)
**Techno :** Node.js · API REST

</details>

<details>
<summary><b>Vitrine Quant Studio</b> · la façade du groupe</summary>

<br>

Le site vitrine de Quant Studio.

**Dépôt :** [`QuantStudioAfrik/vitrine-quant-studio`](https://github.com/QuantStudioAfrik/vitrine-quant-studio)
**Techno :** Next.js · Tailwind · pnpm
**Lancement :** `pnpm install && pnpm dev`

</details>

<details>
<summary><b>OpenDesign</b> · l'outil de design open-source</summary>

<br>

Agent de design + génération d'images.

**Dépôt :** [`QuantStudioAfrik/open-design`](https://github.com/QuantStudioAfrik/open-design) _(slug à confirmer)_
**Techno :** Node · app desktop

</details>

<details>
<summary><b>OpenMontage</b> · la production vidéo agentique</summary>

<br>

Système open-source de production vidéo (pipeline `backlot`).

**Dépôt :** [`QuantStudioAfrik/OpenMontage`](https://github.com/QuantStudioAfrik/OpenMontage) _(slug à confirmer)_
**Techno :** Python

</details>

### 📚 Thesigenix · SaaS académique

<details>
<summary><b>Thesigenix</b> · le copilote des mémoires et des thèses</summary>

<br>

Accompagne étudiants et chercheurs : store de sujets structurés (problématique, revue de littérature, méthodologie), encadrement, gestion multi-rôles (7 rôles).

**Dépôt :** [`QuantStudioAfrik/thesigenix`](https://github.com/QuantStudioAfrik/thesigenix)
**Techno :** Next.js · Express · TypeScript · MongoDB · Docker
**Lancement :** `pnpm install && pnpm dev`

</details>

### 🧩 Infra & outils déployés

Outils open-source tiers qu'on exploite en prod. On ne les écrit pas, on les déploie et on les configure.

<details>
<summary><b>DocuSeal</b> · signature électronique (alternative DocuSign)</summary>

<br>

Branché au module Signature de la Suite.

**Dépôt :** [`QuantStudioAfrik/docuseal`](https://github.com/QuantStudioAfrik/docuseal) _(slug à confirmer)_ · upstream [`docusealco/docuseal`](https://github.com/docusealco/docuseal)

</details>

### 🎓 Quanty Mind

<!-- Aucun dépôt de code à ce jour ; supports de formation hors GitHub. Ajouter ici les dépôts éventuels (notebooks, générateurs d'exercices). -->
_Supports de formation gérés hors GitHub pour l'instant. La place est réservée, elle attend son premier commit._

---

## 8. Qui est qui

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

**Qui contacter avant de paniquer**

| Ton problème | Ta personne |
|---|---|
| Question technique, archi, revue | **Balbine MAMADOU** (Tech Lead) |
| Développement produit au quotidien | **Marthely** |
| Direction, vision, priorités | **David Akpovi** |

<!-- À COMPLÉTER : autres membres, référents par dépôt, contacts (email/chat). -->

---

## 🙋 Autre chose ?

Tu as lu jusqu'ici et un truc manque, cloche, ou est carrément faux ?

1. **Ouvre une PR contre ce README.** C'est littéralement pour ça qu'il existe.
2. Pas sûr·e de la formulation ? Écris-le mal d'abord, la revue polira. Un brouillon moche vaut mille fois mieux qu'un README parfait qui n'existe pas.

Bienvenue à bord. 🎉 Maintenant, va lire le README de ton projet, et essaie de le lancer en local avant le déjeuner. On est ravis de t'avoir.
