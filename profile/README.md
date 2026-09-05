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
> Tu n'as que 15 minutes aujourd'hui ? Lis [comment on bosse](#4-comment-on-bosse), clone ton projet ([section 7](#7-projets--dépôts)) et essaie de le lancer en local. Et si tes attributions te donnent accès au serveur, envoie ta clé SSH ([section 1](#1-se-connecter-à-un-serveur)). Le reste peut dormir jusqu'à demain.

---

## 1. Se connecter à un serveur

> [!CAUTION]
> **L'accès serveur n'est pas automatique.** Tu y as droit uniquement si tes attributions te donnent accès au serveur, après validation du Tech Lead ou de la direction. Sinon, tu n'auras pas d'accès : ce n'est pas un oubli, c'est le principe du moindre privilège. La suite de cette section ne te concerne que si un accès t'a été accordé.

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
- **Les secrets vivent dans Passbolt**, jamais dans git.
- **Front en `pnpm`.** Le lockfile fait foi.
- **Un README par projet** : stack, lancement local, déploiement. Si tu ne sais pas expliquer le démarrage en quelques lignes, c'est ça, le vrai bug.
- **Les règles propres à un projet vivent dans son repo** (dans son `README`). Ici, on ne garde que le général.

</td>
<td width="50%" valign="top">

### ❌ À éviter

- **Pas de secret dans git.** Si ça arrive : fais tourner le secret, *puis* nettoie l'historique. Dans cet ordre.
- **Pas de `npm`/`npx` côté front.** On est en `pnpm`, on y tient.
- **Pas de code sans design approuvé.** On cadre, on valide, *ensuite* on code.

</td>
</tr>
</table>

---

## 5. Workflow Git

> [!IMPORTANT]
> **En bref :** on suit **git-flow** pour les branches et **Conventional Commits** pour les messages. Deux standards, zéro débat à avoir.

### Branches : git-flow

| Branche | Ça sert à quoi | On branche depuis | Ça fusionne dans |
|---|---|---|---|
| `main` | La prod, uniquement des versions taguées | (racine) | (rien) |
| `develop` | L'intégration, là où tout se rejoint | `main` | (via release) |
| `feature/*` | Une fonctionnalité | `develop` | `develop` |
| `release/*` | Préparer une version | `develop` | `main` **et** `develop` |
| `hotfix/*` | Éteindre un feu en prod | `main` | `main` **et** `develop` |

Règle simple : on ne pousse **jamais** en direct sur `main` ni `develop`. Tout passe par une branche et une PR.

### Commits : Conventional Commits

Format : `type(scope): description`, à l'impératif.

```
feat(auth): ajoute le refresh token
fix(paie): corrige l'arrondi CNSS
docs(readme): complète la section serveurs
```

Types courants : `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`. Un changement cassant ? `feat!:` ou un footer `BREAKING CHANGE:`.

Garde-fou : un changement logique par commit. Si ton message a besoin du mot « et », c'est probablement deux commits qui font semblant.

### Pull requests

- Une PR se fait **relire** avant le merge. L'auto-merge en solo, c'est pour les gens qui aiment le rollback du dimanche.
- La description dit : ce qui change, pourquoi, comment c'est testé, et le risque éventuel (migration ? downtime ? breaking change ?).
- Une PR de 2000 lignes n'est pas relue, elle est bénie les yeux fermés. Vise petit.

---

## 6. Secrets & accès

- **Passbolt est notre coffre.** Identifiants, clés d'API, accès serveurs : tout y vit. Jamais dans le code, jamais dans un README, jamais sur le chat. Git n'oublie rien, et c'est bien le problème.
- Le premier jour, demande à ton référent l'accès à l'org GitHub `QuantStudioAfrik` **et** à Passbolt.
- Chaque service qui parle à un autre a un **compte dédié aux droits minimaux**. Pas de compte admin partagé « pour aller plus vite » : c'est comme ça qu'on va très vite dans le mur.

---

## 7. Projets & dépôts

La carte du royaume. **Chaque projet a son propre README dans son dépôt** : c'est là que tu trouves le setup, le déploiement, les variables d'env et les pièges. Ici, c'est juste l'index, pour savoir ce qui existe et qui pinguer.

| Projet | Ce que ça fait | Techno | Dépôt |
|---|---|---|:--|
| 🚩 **Quant Studio Suite** | L'ERP maison : compta, paie, contrats, courrier, signature. Localisations OHADA + Bénin. | `Odoo 19` `Python` `PostgreSQL` `Docker` | [`erp`](https://github.com/QuantStudioAfrik/erp) |
| 📚 **Thesigenix** | Accompagnement mémoires/thèses : store de sujets, encadrement, multi-rôles (7 rôles). | `Next.js` `Express` `TypeScript` `MongoDB` | [`thesigenix`](https://github.com/QuantStudioAfrik/thesigenix) |
| 🤖 **DAO Scanner** | Veille d'appels d'offres : filtre les AO par LLM local et les pousse dans Odoo. | `Python` `Ollama` `Odoo` | [`scanner`](https://github.com/QuantStudioAfrik/scanner) |
| 📰 **Scrapping-Article** | Veille presse : scraping multi-moteurs, alertes, dashboard + API REST. | `Node.js` `REST` | [`scrapping-article`](https://github.com/QuantStudioAfrik/scrapping-article) |
| 🖥️ **Vitrine Quant Studio** | Le site vitrine du groupe. | `Next.js` `Tailwind` `pnpm` | [`vitrine-quant-studio`](https://github.com/QuantStudioAfrik/vitrine-quant-studio) |
| 🎨 **OpenDesign** | Outil de design open-source : agent + génération d'images. | `Node` `desktop` | [`open-design`](https://github.com/QuantStudioAfrik/open-design) ⚠️ |
| 🎬 **OpenMontage** | Production vidéo agentique (pipeline `backlot`). | `Python` | [`OpenMontage`](https://github.com/QuantStudioAfrik/OpenMontage) ⚠️ |

> [!NOTE]
> ⚠️ = slug du dépôt à confirmer. Les **contributeurs** de chaque projet se lisent dans son `git log` : ni une hiérarchie, ni une liste figée. Un nom manquant ou faux ? Ouvre une PR.

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
