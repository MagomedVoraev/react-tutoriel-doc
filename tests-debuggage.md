# Tests

## Mocha - Test runner

[Utilisation de mocha](https://mochajs.org/)

- `describe` permet de définir un chapitre
- `it` permet de définir un test


## Chai - Outil pour faire de l'assertion

[Utilisation de Chai](https://www.chaijs.com/)

- (`assert`), `should`, `expect` : permet d'affirmer quelque chose à vérifier


## Enzyme - Test de composants React

[Utilisation de Enzyme](https://enzymejs.github.io/enzyme/)

- `shallow` permet de faire un pseudo rendu des composants pour tester
- `mount` permet de faire un vrai rendu des composants pour tester


## Comment on installe le tout ?

En faisant les commandes suivantes


```shell
yarn add --dev @babel/register # Pour utiliser la syntaxe d'import ES6 de l'environnement node
yarn add --dev chai mocha enzyme @wojtekmaj/enzyme-adapter-react-17 # assertion / test-runner / test de composants
yarn add --dev ignore-styles # pour ignorer les css quand on test les composants
```


1. Créer un dossier `tests` à la racine du projet

dedans, 2 fichiers :

- `.eslintrc`
```
{
  "env": {
    "mocha": true
  },
  "rules": {
    "no-unused-expressions": "off"
  }
}
```
- `.setup.js`
```js
// Pour pouvoir utiliser les imports
require('@babel/register')();
// Pour pouvoir require des modules react qui ont des imports css
// Sinon il veut interpréter le css comme du JS et ça plante
require('ignore-styles');

const enzyme = require('enzyme');
const Adapter = require('@wojtekmaj/enzyme-adapter-react-17');
enzyme.configure({adapter: new Adapter()})

```


2. Aller dans `package.json`

Dans "scripts", créer une nouvelle commande à la dernière ligne :

```JSON
"test": "cross-env NODE_PATH=./ mocha --require tests/.setup.js './{,!(node_modules)/**/}*.test.js'",
"test:watch": "cross-env NODE_PATH=./ mocha --watch --require tests/.setup.js './{,!(node_modules)/**/}*.test.js'"
```


3. Pour le lancer du coup on fait : `yarn test`


4. toujours dans le dossier tests, créer un dossier reducers :

Dedans : `recipe.test.js` _(recipe = un des reducers qu'on veut tester)_, donc dans ce fichier :

A) On teste que tout fonctionne !

```js
import { expect } from 'chai';

describe('Test describe', () => {
  it('must true return true', () => {
    // on vérifie ici que true est bien égal à true (pour vérifier que tout fonctionne)
    expect(true).to.be.equal(true);
  });
});

```

B) On code nos tests

- on va importer dans ce même fichier le reducer qu'on utilise
- via describe, je décris un chapitre de tests
- permet de s'organiser
- on passe en argument :
  - une chaine de caractères descriptive
  - une fonction de callback contenant le contenu de ce chapitre (sous chapitre + tests)


```js
import { expect } from 'chai';
// on importe le reducer
import recipeReducer from 'src/reducers/recipes';

// via describe je décris un chapitre de tests
// permet de s'organiser
// on passe en arguments :
// - une chaîne de caractère descriptive
// - une fonction de callback contenant le contenu de ce chapitre ( sous chapitre + tests )
describe('reducer for recipes', () => {
  // la structure du reducer
  describe('structure', () => {
    // je décris un test
    // on passe en arguments : 
    // - une chaîne de caractères descriptive
    // - une fonction de callback contenant le/les assertions
    it('must be a function', () => {
      expect(recipeReducer).to.be.a('function');
    });
  });
});
```

Du coup, il y a plusieurs étapes à suivre :

- importer ce qu'on veut tester
- _vérifier que ce qu'on importe est bien exporté_
- déclarer dans un `it('ce que je veux tester',)`
- faire une fonction **callback**
- dans cette fonction j'ai `expect(ceQuiEstImporté).to.be.a(ceQueCaDoitEtreEgalA)`