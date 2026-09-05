# Bienvenue dans l'équipe

Salut, et bienvenue. Si tu lis ça, c'est que tu viens d'être recruté·e — donc que quelqu'un ici t'a fait assez confiance pour te donner un siège sur notre GitHub. Félicitations, et merci d'embarquer. On est vraiment contents de t'avoir.

Ce dépôt existe pour une raison un peu égoïste : que **tu n'aies jamais à demander sur le chat pour comprendre comment on fonctionne**. Tout ce qu'il te faut pour être opérationnel·le dès le premier jour — où vivent les serveurs, comment s'y connecter, ce qu'on édite, qui a écrit quoi, et ce qu'on refusera gentiment en revue — est documenté ici.

Garde cet esprit vivant. Le jour où tu quittes l'équipe, la personne suivante doit pouvoir lire ce même README, sauter la cérémonie du « café d'intro avec le·la senior », et livrer du code dès sa première matinée. Si tu découvres quelque chose qui n'est pas documenté ici, la règle est simple : **documente-le avant de l'oublier**. Le toi du futur remerciera le toi du présent.

Lis à ton rythme, dans l'ordre que tu veux. La table des matières est juste en dessous, et oui, tu pourras revenir plus tard. Personne ne t'interroge dessus.

---

## Ton premier jour, version courte

Si tu n'as que 15 minutes aujourd'hui, fais ces quatre choses dans l'ordre. Le reste peut attendre demain.

1. Génère ta clé SSH et envoie la **publique** à ton référent technique. Voir [section 2](#2-se-connecter-à-un-serveur).
2. Parcours la [section 4 (Principes d'équipe)](#4-principes-déquipe). C'est court. Ça t'évitera une re-revue.
3. Trouve ton projet dans la [section 7](#7-projets--dépôts) et clone son dépôt. Lis **son propre README**.
4. Essaie de le lancer en local. Si tu n'y arrives pas, c'est la première chose à remonter.

> **Bloqué·e sur l'une de ces étapes ?** Demande sur le chat de l'équipe. La seule « question bête » est celle sur laquelle tu restes assis·e trois jours.

---

## Table des matières

1. [Ce qu'on fait](#1-ce-quon-fait)
2. [Se connecter à un serveur](#2-se-connecter-à-un-serveur)
3. [DNS & noms de domaine](#3-dns--noms-de-domaine)
4. [Principes d'équipe (À faire / À éviter / Recommandé)](#4-principes-déquipe)
5. [Workflow Git](#5-workflow-git)
6. [Secrets & accès](#6-secrets--accès)
7. [Projets & dépôts](#7-projets--dépôts)
8. [Qui est qui](#8-qui-est-qui)

---

## 1. Ce qu'on fait

Quant Studio SARL conçoit et édite des logiciels pour le marché africain, l'espace **OHADA** en priorité. Le groupe s'organise en **trois pôles** :

| Pôle | Ce qu'il fait | Nature |
|---|---|---|
| **Teklane** | Ingénierie logicielle : édition de l'ERP, outils métier, veille automatisée, sites | Produits & régie |
| **Thesigenix** | SaaS d'accompagnement à la recherche académique (store de sujets, encadrement) | Produit SaaS |
| **Quanty Mind** | Formation professionnelle : analyse de données, mathématiques, IA | Formation |

Le produit phare, c'est la **Quant Studio Suite** — une suite d'apps Odoo 19 propriétaires (compta, paie, contrats, signature) avec les localisations OHADA et béninoises. Le reste de l'écosystème gravite autour : veille d'appels d'offres, veille presse, sites vitrines, outils internes.

---

## 2. Se connecter à un serveur

**En bref :** clé SSH uniquement. Pas de root, pas de mot de passe. Envoie ta clé **publique** au référent.

### Règles de base (non négociables)

- **Le login root par SSH est désactivé.** Ne le demande pas. Ne l'active pas « juste cinq minutes ». Cinq minutes, c'est comme ça qu'arrivent les intrusions.
- **L'authentification par mot de passe est désactivée.** Oui, même le tien qui est fort. La seule porte d'entrée, c'est une clé SSH.
- **Pas de comptes partagés.** Tu as ton propre utilisateur Unix sur le serveur, avec `sudo` là où c'est justifié.

### Obtenir l'accès (étape par étape)

**Étape 1. Génère ta paire de clés SSH sur ta machine.** Utilise Ed25519 :

```bash
ssh-keygen -t ed25519 -C "prenom@quant-studio"
```

Mets une vraie passphrase. Une clé qui traîne en clair à côté de tes cookies de navigateur ne protège rien.

**Étape 2. Envoie la clé publique au référent.** C'est le fichier qui finit en `.pub` (`~/.ssh/id_ed25519.pub`). Envoie-le sur un canal où le référent peut vérifier que c'est bien toi.

> **N'envoie jamais la clé privée.** Ni sur le chat, ni par mail, ni « juste à toi-même ». Si ça arrive par erreur, régénère une paire et recommence. Aucune honte, juste une rotation.

**Étape 3. Le référent ajoute ta clé** à `~/.ssh/authorized_keys` de l'utilisateur concerné, et te répond avec le nom d'utilisateur et le hostname.

**Étape 4. Connecte-toi :**

```bash
ssh <ton-utilisateur>@<hostname>
```

### Notre infrastructure

<!--
À COMPLÉTER par David / le référent infra. Renseigner les serveurs réels
(hébergeur, plan, OS, rôle, services hébergés). Garder le même format d'une
ligne à l'autre — la cohérence est la seule chose qui nous sépare du chaos.
-->

| Élément | Serveur 1 | Serveur 2 |
|---|---|---|
| Hébergeur | _à préciser_ | _à préciser_ |
| Hostname | _à préciser_ | _à préciser_ |
| OS | _à préciser_ | _à préciser_ |
| Rôle principal | _ex. apps de production_ | _ex. mail / staging / outils_ |
| Services hébergés | _à préciser_ | _à préciser_ |

> **Si tu provisionnes un troisième serveur** (bienvenue au club, on grandit) : copie une colonne et remplis-la. N'invente pas un nouveau format.

---

## 3. DNS & noms de domaine

**En bref :** on décide consciemment `proxied` vs `DNS only`, et on met le DNS en place **avant** la conf nginx (certbot a besoin que le nom résolve déjà).

<!-- À COMPLÉTER : registrar (ex. Hetzner), fournisseur DNS, procédure d'ajout de sous-domaine. Voir le modèle NAYLDIS si besoin. -->

- **Registrar / DNS :** _à préciser_
- **Reverse proxy / TLS :** Nginx + Certbot (Let's Encrypt) devant les conteneurs.

Règles qui font gagner du temps :

- Enregistrements mail (`MX`, SPF, DKIM, DMARC) : jamais proxifiés.
- Quand tu supprimes un service, **supprime aussi son enregistrement DNS.** Les records fantômes, c'est comme ça qu'arrivent les prises de contrôle de sous-domaines.

---

## 4. Principes d'équipe

Ces règles s'appliquent à chaque projet qu'on livre. Elles ne sont pas décoratives : ce sont elles qui rendent nos nuits calmes.

### La stack qu'on utilise

On n'est pas une équipe « on réécrit tout dans le framework de la semaine ». On choisit un petit jeu d'outils et on devient bons dessus.

| Couche | Ce qu'on utilise |
|---|---|
| ERP / métier | **Odoo 19** (Python) |
| Web apps / fronts | **Next.js 16** (React, TypeScript) |
| Services IA / scraping | **Python** (LLM via **Ollama**, Playwright/Cheerio/Puppeteer) |
| Base de données | **PostgreSQL** (Odoo), **MongoDB** (Thesigenix) |
| Conteneurs | **Docker** + **Docker Compose** |
| Reverse proxy / TLS | **Nginx** + **Certbot** |
| Signature électronique | **DocuSeal** (auto-hébergé) |
| Secrets | **Passbolt** |
| Gestionnaire de paquets front | **pnpm** (jamais npm/npx) |

> Envie d'introduire un nouvel outil ? Ouvre une discussion d'abord. La barre n'est pas « est-ce que c'est cool », c'est « est-ce que ça vaut le deuxième outil qu'on devra désormais patcher, monitorer et enseigner aux nouveaux ».

### ✅ À faire

- **Toujours dockeriser.** Chaque projet tourne en conteneurs, avec un `docker-compose.yml`. L'hôte reste propre.
- **Pas de code sans design approuvé.** C'est notre règle d'or. On cadre, on valide, ensuite on code.
- **Écrire un README** par projet : stack, comment lancer en local, comment déployer. Si tu ne peux pas expliquer le démarrage en 10 lignes, c'est ça le bug.
- **Gérer les secrets proprement** (Passbolt, fichiers env hors git). Jamais dans un commit. Jamais.
- **Sauvegarder.** Dumps de base, configs, volumes : automatisés, hors serveur, et testés en restaurant de temps en temps.

### ❌ À éviter

- **Ne pousse pas sur `main` directement.** Ouvre une PR. Même seul·e sur le projet.
- **Ne livre pas de secret dans git.** Si ça arrive : fais tourner le secret, puis nettoie l'historique. Dans cet ordre.
- **Ne réinvente pas ton auth, ta crypto ni ta file d'attente.** Ce qui existe marche.
- **Ne désactive pas la vérification SSL « pour debugger ».** La minute où ça part en prod avec `verify=False`, ça y reste.
- **N'ajoute pas une dépendance pour un one-liner.** Dans cinq ans, quelqu'un patchera sa 17e vulnérabilité transitive.

### Recommandé (fortes suggestions, pas des lois)

- **Lis la doc de l'outil avant de demander.** Puis demande — on répond volontiers, juste pas à la question qui est le premier paragraphe du README.
- **Les PR les plus petites possibles.** Une PR de 2000 lignes n'est pas revue, elle est tamponnée.
- **Commente le _pourquoi_, pas le _quoi_.** Un bon nommage explique le quoi.
- **Sois bienveillant·e en revue.** On revoit le code, pas la personne.

### Notre outillage de dev : super-dev

Le développement suit le framework interne **super-dev** (plugin Claude Code) :

| Étape | Commande | Quand |
|---|---|---|
| Dérouler une feature de bout en bout | `/build` | Toute nouvelle fonctionnalité |
| Vérifier avant commit | `/verify` | Avant chaque commit |
| Passe d'authenticité (style) | `/ghostwrite` | Avant de livrer |
| Revue de sécurité | `/security` | Sur toute surface sensible |
| Idée hors-scope | `/backlog` | Ce qui sort du périmètre |

Les licences du code produit : **QSEL-1.0** (Quant Studio Edition License) sauf mention contraire — voir le `LICENSE` de chaque dépôt.

---

## 5. Workflow Git

**En bref :** branche depuis `main`, ouvre une PR, attends une revue et une CI verte, squash au merge.

### Branches

- `main` est toujours déployable. La prod suit `main` (ou un tag coupé dessus).
- Fonctionnalités : `feat/<description-courte-kebab>`.
- Correctifs : `fix/<description-courte-kebab>`.

### Commits

- Mode impératif : « Ajoute l'endpoint de matching », pas « Ajouté » ni « Ajoute et corrige ».
- Un changement logique par commit. Si le message a besoin du mot « et », c'est probablement deux commits.

### Pull requests

- **Au moins une revue approuvée** avant le merge. Pas d'auto-merge.
- **La CI doit être verte.** Pas d'exception, pas de « je corrige après le merge ».
- **La description dit :** ce qui change, pourquoi, comment ça a été testé, et le risque éventuel (migration ? downtime ? breaking change ?).
- **Supprime la branche** après le merge. Elle est dans `main` maintenant.

---

## 6. Secrets & accès

- **Passbolt** est notre coffre. Les identifiants, clés d'API et accès serveurs y vivent — jamais dans le code, jamais dans un README, jamais sur le chat.
- Demande à ton référent l'accès à l'org GitHub `QuantStudioAfrik` et à Passbolt le premier jour.
- Chaque service qui parle à un autre a un **compte dédié aux droits minimaux**. Pas de compte admin partagé « pour aller plus vite ».

---

## 7. Projets & dépôts

Carte rapide de ce qui existe. **Chaque projet a son propre README dans son dépôt** — c'est là que tu vas pour le setup, le déploiement, les variables d'env et les pièges. Cette section est juste l'index, pour savoir ce qui existe et qui pinguer.

> Les **contributeurs** viennent du `git log` de chaque dépôt. Ce n'est ni une hiérarchie ni exhaustif. Un nom manquant ou faux ? Ouvre une PR. C'est tout l'intérêt.

### 🛠️ Teklane — ingénierie logicielle

**Quant Studio Suite (ERP)** — suite d'apps Odoo 19 propriétaires : compta, paie, contrats (CLM), courrier, signature. Localisations OHADA (17 pays) + Bénin (CNSS/IPRES/IRPP, DGI). Produit phare.
- **Dépôt :** [`QuantStudioAfrik/erp`](https://github.com/QuantStudioAfrik/erp) · **Stack :** Odoo 19 · Python · PostgreSQL · Docker · **Lancement :** `docker compose up -d` → `http://localhost:8082`

**DAO Scanner** — robot de veille d'appels d'offres : ratisse les portails de marchés publics, juge chaque AO via LLM (Ollama), pousse les projets d'ingénierie logicielle dans Odoo (`crm.ao`).
- **Dépôt :** [`QuantStudioAfrik/scanner`](https://github.com/QuantStudioAfrik/scanner) · **Stack :** Python · Ollama · Odoo

**Scrapping-Article** — veille presse full-stack : scraping multi-moteurs, suivi de mots-clés, alertes, dashboard + API REST, exports CSV/XLSX.
- **Dépôt :** [`QuantStudioAfrik/scrapping-article`](https://github.com/QuantStudioAfrik/scrapping-article) · **Stack :** Node.js · REST

**Vitrine Quant Studio** — site vitrine du groupe.
- **Dépôt :** [`QuantStudioAfrik/vitrine-quant-studio`](https://github.com/QuantStudioAfrik/vitrine-quant-studio) · **Stack :** Next.js 16 · Tailwind v4 · pnpm · **Lancement :** `pnpm install && pnpm dev`

**OpenDesign** — alternative open-source à Claude Design (agent de design + génération d'images).
- **Dépôt :** [`QuantStudioAfrik/open-design`](https://github.com/QuantStudioAfrik/open-design) _(slug à confirmer)_ · **Stack :** Node · app desktop

**OpenMontage** — système agentique open-source de production vidéo (pipeline `backlot`).
- **Dépôt :** [`QuantStudioAfrik/OpenMontage`](https://github.com/QuantStudioAfrik/OpenMontage) _(slug à confirmer)_ · **Stack :** Python

### 📚 Thesigenix — SaaS académique

**Thesigenix** — accompagnement des étudiants et chercheurs : store de sujets structurés (problématique, revue de littérature, méthodologie), encadrement, gestion multi-rôles (7 rôles).
- **Dépôt :** [`QuantStudioAfrik/thesigenix`](https://github.com/QuantStudioAfrik/thesigenix) · **Stack :** Next.js 16 · TypeScript · MongoDB · Docker · **Lancement :** `pnpm install && pnpm dev`

### 🧩 Infra & outils déployés

Outils open-source tiers qu'on exploite en production. On ne les édite pas, on les déploie/configure.

**DocuSeal** — signature électronique de documents (alternative DocuSign), branchée au module Signature de la Suite.
- **Dépôt :** [`QuantStudioAfrik/docuseal`](https://github.com/QuantStudioAfrik/docuseal) _(slug à confirmer)_ · upstream [`docusealco/docuseal`](https://github.com/docusealco/docuseal)

### 🎓 Quanty Mind

<!-- Aucun dépôt de code à ce jour ; supports de formation gérés hors GitHub. Ajouter ici les dépôts éventuels (notebooks, générateurs d'exercices). -->
_Supports de formation gérés hors GitHub pour l'instant._

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

**Qui contacter pour quoi**

- **Question technique / architecture / revue** → **Balbine MAMADOU** (Tech Lead)
- **Développement produit au quotidien** → **Marthely**
- **Direction / vision / priorités** → **David Akpovi**

<!-- À COMPLÉTER : autres membres, référents par dépôt, contacts (email/chat). -->

---

## Autre chose ?

Si tu as lu jusqu'ici et que quelque chose manque, n'est pas clair, ou est carrément faux :

1. Ouvre une PR contre ce README. C'est littéralement pour ça qu'il existe.
2. Pas sûr·e de la formulation ? Écris-le mal d'abord, la revue corrigera. Un mauvais brouillon vaut mieux qu'un README parfait qui n'existe pas.

Bienvenue à bord. Maintenant va lire le README du projet qui t'a été confié, et essaie de le lancer en local avant le déjeuner. On est contents de t'avoir.
