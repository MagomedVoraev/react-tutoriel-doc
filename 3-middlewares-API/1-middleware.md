# Middlewares - API

[Fiches Récap KOUROU](https://kourou.oclock.io/ressources/fiche-recap/redux-avance/#appliquer-un-middleware)

Un middleware est un triple fléchée : une fonction qui retourne une fonction qui retourne une fonction :
```js
export default store => next => (action) => {
// ...
// store : store de redux, on pourra utiliser store.getState() et store.dispatch()

// next : il s'agit du middleware suivant, il faudra exécuter cette fonction en lui passant action, pour qu'il puisse lui aussi traiter l'action comme il le souhaite

// action : l'action qui vient d'être dispatchée
}
```

1. Créer un dossier `middleware` dans `src/`

2. Créer autant de `fichier.js` qu'on en a besoin _(un middleware par logique)_

Dans notre exemple on crée un fichier `auth.js`

```js
export default (store) => (next) => (action) => {
    // ...on fait notre traitement ici
    switch (action.type) {
      // case NOM_ACTION:
      // ...
      // ...

    }
    // et on passe au voisin
    // NE PAS OUBLIER LE MOT RETURN
    // meme si dans ce cas précis il n'est pas nécessaire
    // il nous arrivera d'en avoir besoin obligatoirement (le return)
    // donc autant l'écrire tout le temps selon @Sebastien
    return next(action)
}
```

3. Importer `applyMiddleware` ET `compose` du redux dans le `store/index.js`

```js
// le createStore est déjà importée par défaut lorsqu'on fait notre store Redux, 
// là, on ajoute EN PLUS le applyMiddleware
```


4. Puis, toujours dans `store/index.js` importer le `middleware`
```js
// le nom de ce qu'on importe est une convention, on met le nom du fichier d'abord puis on précise
// en camelCase que c'est un middleware
```


5. On utilise le `auth`+`Enhancer` en le passant à `applyMiddleware`
```js
// 'auth' est le nom de notre fichier dans middleware et on rajoute Enhancer par convention
// applyMiddleware est une fonction de redux qu'on a importé en haut
// authMiddleware est LE middleware qu'on a créé et importé en haut
```

6. On déclare le tout dans le `STORE`


7. CODE FINAL : 

```js
/* eslint-disable no-underscore-dangle */
import { createStore, applyMiddleware, compose } from 'redux';
import authMiddleware from 'src/middleware/auth';
import reducer from './reducer';

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

// On créé le store en lui donnant le reducer afin transformer les actions
// en changement d'état, et pour calculer aussi l'état initial
const store = createStore(
  reducer, /* preloadedState, */
  composeEnhancers(
    applyMiddleware(
      authMiddleware,
    ),
  ),
);

export default store;
```

[COURS numéro 3 arrêté à 47min20sec](https://drive.google.com/drive/folders/1g3f5hAHrBvtE8FlvtwMR78ZZVXDqxX_4)