# 👋 Bienvenue dans l'équipe

Salut, et bienvenue. Si tu lis ça, c'est que tu viens d'être recruté·e, donc que quelqu'un ici t'a fait assez confiance pour te donner un siège sur notre GitHub. Félicitations, et merci d'embarquer. On est vraiment contents de t'avoir (et pas seulement parce qu'on avait besoin de bras).

Ce dépôt existe pour une raison un peu égoïste : que **tu n'aies jamais à déranger quelqu'un sur le chat pour comprendre comment on fonctionne**. Où vivent les serveurs, comment s'y connecter, ce qu'on fabrique, qui a écrit quoi, et ce qu'on refusera gentiment en revue : tout est ici.

Garde cet esprit vivant. Le jour où tu quittes l'équipe, la personne suivante doit pouvoir lire ce même README, sauter la cérémonie du « café d'intro avec le·la senior », et livrer du code dès sa première matinée. Si tu découvres un truc qui n'est pas documenté ici, la règle tient en trois mots : **documente-le avant de l'oublier**. Le toi du futur t'offrira une bière pour ça.

Lis à ton rythme, dans l'ordre que tu veux. La table des matières est juste en dessous. Et non, il n'y a pas d'examen à la fin.

---

## 🚀 Ton premier jour, version courte

Tu n'as que 15 minutes aujourd'hui ? Fais ces quatre choses, dans l'ordre. Le reste peut dormir jusqu'à demain.

1. **Génère ta clé SSH** et envoie la **publique** à ton référent technique. Voir [section 2](#2-se-connecter-à-un-serveur).
2. **Parcours la [section 4 (Principes d'équipe)](#4-principes-déquipe).** C'est court, et ça t'évitera de te faire renvoyer ta première PR.
3. **Trouve ton projet** dans la [section 7](#7-projets--dépôts), clone son dépôt, et lis **son propre README**.
4. **Essaie de le lancer en local.** Si ça refuse de démarrer, félicitations : tu as trouvé ta première tâche.

> [!TIP]
> Bloqué·e sur une de ces étapes ? Demande sur le chat de l'équipe. La seule vraie question bête, c'est celle sur laquelle tu restes assis·e trois jours en silence.

---

## 🗺️ Table des matières

| # | Section | En un mot |
|:-:|---|---|
| 1 | [Ce qu'on fait](#1-ce-quon-fait) | Le pourquoi de tout ça |
| 2 | [Se connecter à un serveur](#2-se-connecter-à-un-serveur) | Ta clé, tes accès |
| 3 | [DNS & noms de domaine](#3-dns--noms-de-domaine) | Où pointent les flèches |
| 4 | [Principes d'équipe](#4-principes-déquipe) | À faire / à éviter / recommandé |
| 5 | [Workflow Git](#5-workflow-git) | Branche, PR, merge, répète |
| 6 | [Secrets & accès](#6-secrets--accès) | Le coffre, et pourquoi git n'en est pas un |
| 7 | [Projets & dépôts](#7-projets--dépôts) | La carte du royaume |
| 8 | [Qui est qui](#8-qui-est-qui) | À qui parler avant de paniquer |

---

## 1. Ce qu'on fait

Quant Studio SARL conçoit et édite des logiciels pour le marché africain, l'espace **OHADA** en priorité. Le groupe tient sur **trois pôles** :

| Pôle | Ce qu'il fait | Nature |
|---|---|---|
| 🛠️ **Teklane** | Ingénierie logicielle : l'ERP, les outils métier, la veille automatisée, les sites | Produits & régie |
| 📚 **Thesigenix** | SaaS d'accompagnement à la recherche académique (store de sujets, encadrement) | Produit SaaS |
| 🎓 **Quanty Mind** | Formation pro : analyse de données, mathématiques, IA | Formation |

Le vaisseau amiral, c'est la **Quant Studio Suite** : une suite d'apps Odoo 19 propriétaires (compta, paie, contrats, signature) taillée pour l'OHADA et le Bénin. Tout le reste gravite autour : veille d'appels d'offres, veille presse, sites vitrines, outils internes. Bref, on ne s'ennuie pas.

---

## 2. Se connecter à un serveur

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

### Notre infrastructure

<!--
À COMPLÉTER par David / le référent infra. Renseigner les serveurs réels
(hébergeur, plan, OS, rôle, services). Garder le même format d'une colonne
à l'autre : la cohérence est la seule chose qui nous sépare du chaos.
-->

| Élément | Serveur 1 | Serveur 2 |
|---|---|---|
| Hébergeur | _à préciser_ | _à préciser_ |
| Hostname | _à préciser_ | _à préciser_ |
| OS | _à préciser_ | _à préciser_ |
| Rôle principal | _ex. apps de production_ | _ex. mail / staging / outils_ |
| Services hébergés | _à préciser_ | _à préciser_ |

> [!NOTE]
> Tu provisionnes un troisième serveur ? Bienvenue au club, on grandit. Copie une colonne et remplis-la. N'invente **pas** un nouveau format : le futur toi qui relit ce tableau à 2h du matin te remerciera.

---

## 3. DNS & noms de domaine

> [!IMPORTANT]
> **En bref :** on choisit consciemment `proxied` ou `DNS only`, et on pose le DNS **avant** la conf nginx. Certbot a besoin que le nom résolve déjà, il n'est pas devin.

<!-- À COMPLÉTER : registrar, fournisseur DNS, procédure d'ajout de sous-domaine. Voir le modèle NAYLDIS au besoin. -->

- **Registrar / DNS :** _à préciser_
- **Reverse proxy / TLS :** Nginx + Certbot (Let's Encrypt) devant les conteneurs.

Deux règles qui font gagner des heures :

- **Mail** (`MX`, SPF, DKIM, DMARC) : jamais proxifié. Le proxy et le mail ne s'aiment pas.
- **Tu supprimes un service ? Supprime son enregistrement DNS.** Un record fantôme qui pointe vers un serveur qu'on ne contrôle plus, c'est le tapis rouge d'une prise de contrôle de sous-domaine.

---

## 4. Principes d'équipe

Ces règles s'appliquent à chaque projet qu'on livre. Elles ne sont pas là pour décorer : ce sont elles qui rendent nos nuits calmes et nos week-ends sans astreinte surprise.

### La stack qu'on utilise

On n'est pas l'équipe « on réécrit tout dans le framework de la semaine ». On choisit un petit jeu d'outils, et on devient bons dessus.

| Couche | Ce qu'on utilise |
|---|---|
| ERP / métier | **Odoo 19** (Python) |
| Web apps / fronts | **Next.js 16** (React, TypeScript) |
| Services IA / scraping | **Python** (LLM via **Ollama**, Playwright / Cheerio / Puppeteer) |
| Base de données | **PostgreSQL** (Odoo), **MongoDB** (Thesigenix) |
| Conteneurs | **Docker** + **Docker Compose** |
| Reverse proxy / TLS | **Nginx** + **Certbot** |
| Signature électronique | **DocuSeal** (auto-hébergé) |
| Secrets | **Passbolt** |
| Paquets front | **pnpm** (jamais npm/npx, on y tient) |

> [!NOTE]
> Envie d'ajouter un nouvel outil ? Ouvre une discussion d'abord. La barre n'est pas « est-ce que c'est cool » (tout est cool le vendredi soir), c'est « est-ce que ça vaut le deuxième outil qu'on devra patcher, monitorer et expliquer à chaque nouveau ».

<table>
<tr>
<td width="50%" valign="top">

### ✅ À faire

- **Toujours dockeriser.** Un `docker-compose.yml`, et l'hôte reste propre.
- **Pas de code sans design approuvé.** Notre règle d'or. On cadre, on valide, *ensuite* on code.
- **Écrire un README** par projet : stack, lancement local, déploiement. Si tu ne sais pas expliquer le démarrage en 10 lignes, c'est ça, le vrai bug.
- **Gérer les secrets proprement** (Passbolt, env hors git). Jamais dans un commit. Jamais.
- **Sauvegarder.** Dumps, configs, volumes : automatisés, hors serveur, et *testés* en restaurant de temps en temps. Une sauvegarde jamais restaurée est une hypothèse, pas une sauvegarde.

</td>
<td width="50%" valign="top">

### ❌ À éviter

- **Pousser sur `main` en direct.** Ouvre une PR. Même seul·e. Surtout seul·e.
- **Livrer un secret dans git.** Si ça arrive : fais tourner le secret, *puis* nettoie l'historique. Dans cet ordre.
- **Réinventer l'auth, la crypto ou la file d'attente.** Ce qui existe marche et a déjà été audité par plus malin que nous.
- **Désactiver la vérif SSL « pour debugger ».** La minute où ça part en prod avec `verify=False`, ça y reste pour cinq ans.
- **Ajouter une dépendance pour un one-liner.** Un jour, quelqu'un (probablement toi) patchera sa 17e vulnérabilité transitive.

</td>
</tr>
</table>

### 💡 Recommandé (fortes suggestions, pas des lois)

- **Lis la doc de l'outil avant de demander.** Puis demande, avec plaisir. On répond volontiers à tout, sauf à la question qui est littéralement le premier paragraphe du README.
- **Les PR les plus petites possibles.** Une PR de 2000 lignes n'est pas relue, elle est bénie les yeux fermés.
- **Commente le _pourquoi_, pas le _quoi_.** Un bon nommage explique déjà le quoi.
- **Sois sympa en revue.** On critique le code, pas la personne. Et on attend la même énergie quand c'est ton tour de recevoir les remarques.

### 🧰 Notre outillage : super-dev

Le dev suit le framework interne **super-dev** (plugin Claude Code) :

| Étape | Commande | Quand |
|---|---|---|
| Dérouler une feature de bout en bout | `/build` | Toute nouvelle fonctionnalité |
| Vérifier avant commit | `/verify` | Avant chaque commit |
| Passe d'authenticité (style) | `/ghostwrite` | Avant de livrer |
| Revue de sécurité | `/security` | Sur toute surface sensible |
| Idée hors-scope | `/backlog` | Ce qui déborde du périmètre |

Côté licences : le code produit est sous **QSEL-1.0** (Quant Studio Edition License), sauf mention contraire dans le `LICENSE` du dépôt.

---

## 5. Workflow Git

> [!IMPORTANT]
> **En bref :** branche depuis `main`, ouvre une PR, attends une revue et une CI verte, squash au merge. C'est tout. Vraiment.

**Branches**
- `main` est toujours déployable. La prod suit `main` (ou un tag coupé dessus).
- Fonctionnalités : `feat/<description-courte-kebab>`
- Correctifs : `fix/<description-courte-kebab>`

**Commits**
- Mode impératif : « Ajoute l'endpoint de matching », pas « Ajouté », pas « des trucs ».
- Un changement logique par commit. Si ton message a besoin du mot « et », c'est probablement deux commits qui font semblant.

**Pull requests**
- **Au moins une revue approuvée** avant le merge. L'auto-merge, c'est pour les gens qui aiment le risque et le rollback.
- **CI verte, sans exception.** Pas de « je corrige après le merge » (spoiler : personne ne corrige après le merge).
- **La description dit :** ce qui change, pourquoi, comment c'est testé, et le risque éventuel (migration ? downtime ? breaking change ?).
- **Supprime la branche** après le merge. Son travail est dans `main`, laisse-la partir en paix.

---

## 6. Secrets & accès

- **Passbolt est notre coffre.** Identifiants, clés d'API, accès serveurs : tout y vit. Jamais dans le code, jamais dans un README, jamais sur le chat. Git n'oublie rien, et c'est bien le problème.
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
**Stack :** Odoo 19 · Python · PostgreSQL · Docker
**Lancement :** `docker compose up -d` puis le backoffice sur `http://localhost:8082`

</details>

<details>
<summary><b>DAO Scanner</b> · le robot qui lit les appels d'offres à ta place</summary>

<br>

Ratisse les portails de marchés publics, juge chaque AO via un LLM (Ollama), et ne garde que les projets d'ingénierie logicielle qu'il pousse dans Odoo (`crm.ao`).

**Dépôt :** [`QuantStudioAfrik/scanner`](https://github.com/QuantStudioAfrik/scanner)
**Stack :** Python · Ollama · Odoo

</details>

<details>
<summary><b>Scrapping-Article</b> · la veille presse full-stack</summary>

<br>

Scraping multi-moteurs, suivi de mots-clés, alertes, dashboard + API REST, exports CSV/XLSX.

**Dépôt :** [`QuantStudioAfrik/scrapping-article`](https://github.com/QuantStudioAfrik/scrapping-article)
**Stack :** Node.js · REST

</details>

<details>
<summary><b>Vitrine Quant Studio</b> · la façade du groupe</summary>

<br>

Le site vitrine de Quant Studio.

**Dépôt :** [`QuantStudioAfrik/vitrine-quant-studio`](https://github.com/QuantStudioAfrik/vitrine-quant-studio)
**Stack :** Next.js 16 · Tailwind v4 · pnpm
**Lancement :** `pnpm install && pnpm dev`

</details>

<details>
<summary><b>OpenDesign</b> · l'alternative open-source à Claude Design</summary>

<br>

Agent de design + génération d'images.

**Dépôt :** [`QuantStudioAfrik/open-design`](https://github.com/QuantStudioAfrik/open-design) _(slug à confirmer)_
**Stack :** Node · app desktop

</details>

<details>
<summary><b>OpenMontage</b> · la production vidéo agentique</summary>

<br>

Système open-source de production vidéo (pipeline `backlot`).

**Dépôt :** [`QuantStudioAfrik/OpenMontage`](https://github.com/QuantStudioAfrik/OpenMontage) _(slug à confirmer)_
**Stack :** Python

</details>

### 📚 Thesigenix · SaaS académique

<details>
<summary><b>Thesigenix</b> · le copilote des mémoires et des thèses</summary>

<br>

Accompagne étudiants et chercheurs : store de sujets structurés (problématique, revue de littérature, méthodologie), encadrement, gestion multi-rôles (7 rôles).

**Dépôt :** [`QuantStudioAfrik/thesigenix`](https://github.com/QuantStudioAfrik/thesigenix)
**Stack :** Next.js 16 · TypeScript · MongoDB · Docker
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
