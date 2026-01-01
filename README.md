# UE L313 — Projet Symfony (Watson-like) : Gestion de liens (CRUD)

Ce dépôt contient un projet **Symfony 6.4 LTS** réalisé en groupe dans le cadre de l’**UE L313**.
L’objectif est de proposer un socle de fonctionnalités proches du projet *Watson* : **gestion de liens stockés en base de données** (liste, ajout, modification, suppression).

---

## Fonctionnalités (minimum demandé)

- ✅ Listing des liens en base de données
- ✅ Ajout d’un lien via formulaire (un lien contient : **titre**, **URL**, **descriptif**)
- ✅ Mise à jour d’un lien
- ✅ Suppression d’un lien

CRUD disponible via le contrôleur `src/Controller/LienController.php` (routes préfixées par `/lien`).

---

## Pré-requis

- **PHP 8.2+** (recommandé : le `composer.lock` du projet est compatible avec 8.2+)
- **Composer**
- **MySQL / MariaDB**

> Vérifier avec : `php -v`

---

## Installation

### 1) Cloner le dépôt
```bash
git clone https://github.com/allegronontropo/watson-symfony.git
cd watson-symfony
```

### 2) Installer les dépendances
```bash
composer install
```

### 3) Configurer l’environnement (.env)
Le fichier `.env` n’est pas versionné.
1. Copier `.env.example` en `.env`
2. Mettre à jour la variable `DATABASE_URL` selon votre environnement

Exemple (WAMP par défaut, sans mot de passe) :
```env
DATABASE_URL="mysql://root:@127.0.0.1:3306/uel313?serverVersion=8.0"
```

---

## Base de données

### 1) Créer la base
```bash
php bin/console doctrine:database:create
```

### 2) Créer les tables
À l’état actuel, le projet ne contient pas encore de migrations enregistrées.
Pour créer le schéma à partir des entités Doctrine :

```bash
php bin/console doctrine:schema:update --force
```

> (Optionnel) Voir le SQL généré avant d’appliquer :
> `php bin/console doctrine:schema:update --dump-sql`

---

## Lancer le projet

### Méthode recommandée (serveur PHP natif)
Cette méthode évite les problèmes de réécriture d’URL Apache (Rewrite/.htaccess) sur WAMP.

Depuis la racine du projet :
```bash
php -S 127.0.0.1:8000 -t public
```

Puis ouvrir :
- CRUD liens : http://127.0.0.1:8000/lien

---

## Routes utiles

- `/lien` : liste des liens
- `/lien/new` : ajout
- `/lien/{id}` : détail
- `/lien/{id}/edit` : édition
- Suppression : formulaire POST sur `/lien/{id}` (CSRF)

Pour lister toutes les routes disponibles :
```bash
php bin/console debug:router
```

