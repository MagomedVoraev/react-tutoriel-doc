# Projet

## Gestionnaire de modules / dépendances

> Récupérer, lister, gérer, nos dépendances

**package.json** : fiche d'identité du projet
- auteur
- nom
- repo
- dépendances
- scripts
- ressources diverses (configuration, notes, ...)
- ...

### npm : l'outil par défaut pour les modules autour de node

> Gestion des dépendances et du projet

**Initialiser le projet : package.json**

`npm init`

**Installation de dépendance**

> Dépendance de projet : dépendance utilisée dans le code (react, axios, redux, ...)

- Télécharger la dépendance dans un dossier du projet : `node_modules` (le dossier node_modules ne doit pas être pushé)
- Ajoute la dépendance dans les "dépendances de projet"

`npm install laDépendance`

> Dépendance de développement : dépendances utilisées uniquement pour la phase de dev (bundler, linter, outils de tests, ...)

- Ajoute la dépendance dans les "dépendances de développement"

`npm install --save-dev laDépendanceDeDev`

**Rappatrier les dépendances sauvegardées**

- création du dossier `node_modules`
- recup des dépendances listées

`npm install`

### yarn : npm sous vitamines

> même travail que npm avec en plus : syntaxe plus cohérente, plus rapide (cache), plus kikoolol : icones, barre de progression, ... :D

**Initialiser le projet : package.json**

`yarn init`

**Installation de dépendance**

> Dépendance de projet : dépendance utilisée dans le code (react, axios, redux, ...)

- Télécharger la dépendance dans un dossier du projet : `node_modules` (le dossier node_modules ne doit pas être pushé)
- Ajoute la dépendance dans les "dépendances de projet"

`yarn add laDépendance`

> Dépendance de développement : dépendances utilisées uniquement pour la phase de dev (bundler, linter, outils de tests, ...)

- Ajoute la dépendance dans les "dépendances de développement"

`yarn add --dev laDépendanceDeDev`

**Rappatrier les dépendances sauvegardées**

- création du dossier `node_modules`
- recup des dépendances listées

`yarn`


## Bundler : webpack

> https://webpack.js.org/

- Lire et centraliser les contenus
- Appliquer des outils annexes (babel, node-sass)
- Gérer tous les types de fichiers pour la phase de développement
- Compression et adaptation pour la phase de production
  - css minifié
  - js compatible, nettoyé, minifié
  - organisation de ficher propre (le moins de fichier / rangement optimisé)

## Transpiler : babel

> https://babeljs.io/

- Transforme le code ES6 vers une version compatible avec tous les navigateurs
- Comprend et transforme le code JSX (sucre syntaxique pour React) en JavaScript classique
- Son travail est déclenché par `webpack`
