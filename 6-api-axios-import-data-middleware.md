# API - Middleware

[Fiches Récap KOUROU](https://kourou.oclock.io/ressources/fiche-recap/redux-avance/#appliquer-un-middleware)

1. Dans le `MainComponent`

- déclarer un `useEffect` avant le `return` du JSX
- mettre dedans une fonction `fetchData()`
- déclarer la même fonction en **props + en propTypes** du MainComponent

```js
// déclarer en props
const App = ({ fetchData }) => {
//...
//...
  // utiliser le useEffect
  useEffect(() => {
    // On demande à récupérer la donnée
    // Pour ca je dois donc déclencher une intention de récupération de données
    // déclarer une fonction qui sera lancée PUIS la déclarer en props + propTypes
    fetchData();
  }, []);


//...
//...
App.propTypes = {
  fetchRecipes: PropTypes.func.isRequired
};
}
```


2. Créer un dossier `src/actions`

- créer un fichier `index.js`
- utiliser le snippet `action`
- donner le MEME NOM de fonction que celle utilisée _(appelée)_ dans le useEffect() du MainComponent

```js
export const GET_DATA = 'GET_DATA';

export const getData = () => ({
  type: GET_DATA,

});
```


3. Créer dans `src/containers` un dossier `App/index.js`

- utiliser snippet `container`
- aller dans la fonction de `dispatch`
- importer la fonction déclarée dans ACTION
- à gauche, je donne le nom de la fonction utilisée dans le MAINCOMPONENT, et à droite celle DECLARÉE dans ACTION

```js
import { connect } from 'react-redux';
import App from 'src/components/App';
// j'importe la fonction ACTION CREATOR
import { getData } from 'src/actions';

const mapStateToProps = (state) => ({
});

const mapDispatchToProps = (dispatch) => ({
    // à gauche la fonction déclanchée dans le MainComponent
    // .............à droite, getData() celle déclarée dans ACTION
    fetchData: () => dispatch(getData()),
});

export default connect(mapStateToProps, mapDispatchToProps)(App);
```


4. RENDER : main `index.js`

- aller dans le main index.js
- changer le COMPONENTS de `import App from 'src/components/App';` PAR `containers` => `import App from 'src/components/App`

```js
import React from 'react';
import ReactDom from 'react-dom';
import { Provider } from 'react-redux';
// on change ici par containers (à la base est components)
import App from 'src/containers/App';

import store from 'src/store';

const rootReactElement = (
  <Provider store={store}>
      <App />
  </Provider>
);

const target = document.getElementById('root');

ReactDom.render(rootReactElement, target);
```


**On peut maintenant aller sur le navigateur, lancer le localhost, et vérifier avec redux dev-tools si l'action type est bien lancée : GET_DATA dans notre cas, et à l'intérieur, state: []**


5. Créer un dossier `src/middlewares/data.js`

- utiliser snippet `middleware`
- importer l'action type qui vient


```js
import { GET_DATA, setRecipes } from 'src/actions/recipes';

export default (store) => (next) => (action) => {
    // ... ce qu'il y a dedas, sera vu plus tard, on va le rajouter lors de l'étape 8
};
```


6. Dans `store/index.js`

- _s'assurer que c'est bien le store avec utilisation de snippet `storemiddleware`_
- importer le `middleware` qui vient d'être crée

```js
import { createStore, applyMiddleware, compose } from 'redux';
import dataMiddleware from 'src/middlewares/data';
// on importe le dossier reducers
import reducer from './reducer';

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

// On créé le store en lui donnant le reducer afin transformer les actions
// en changement d'état, et pour calculer aussi l'état initial

const enhancers = composeEnhancers(
  applyMiddleware(
    dataMiddleware,
  ),
);

const store = createStore(reducer, enhancers);

export default store;
```


7. Créer `src/api/index.js`

- `yarn add axios`
- `import axios from 'axios';`
- déclarer fonction de axios :

```js
import axios from 'axios';

export default axios.create({
  baseURL: 'http://localhost:3001',
  timeout: 1000,
});
```


8. Dans `src/actions/index.js`

- utiliser snippet `action` pour ajouter une nouvelle action
- nouvelle action : `setData(data)` _(qui sera utilisé lors de la requete axios en dispatch)_

```js
export const SET_DATA = 'SET_DATA';

export const setData = (data) => ({
  type: SET_DATA,
  data,
});
```


9. On revient dans `src/middlewares/data` de l'étape **5**

- on importe axios src/api
- on importe les actions types depuis src/actions
- on déclare les CASE en utilisant les actions types
- importer l'ACTION CREATOR qui sera utilisée pour le dispatch
```js
// j'importe ACTION et son fichier
// setData = action creator
import { GET_DATA, setData } from 'src/actions/';
import axios from 'src/api';

export default (store) => (next) => (action) => {
  // Si nous voulons traiter des données de state qui sont dans store,
  // il faut les décomposer ici en utilisant la fonction getState() de redux :
  // ex: on récupère email et password qui sont dans l'objet settings qui sont dans le store/reducer
  const { settings: { email, password } } = store.getState();
  // l'exemple d'en haut store.getState() n'a pas de rapport direct notre axios
  
  console.log('je suis dans le middleware');
  switch (action.type) {
    case GET_DATA:
      axios.get('/recipes')
      .then((result) => {
        // utilisation de l'action crée étape 8 avec son paramètre data (ACTION CREATOR)
        // ce qui est dans result.data sera envoyé dans "data" le paramètre déclaré dans l'action setData(data)
        store.dispatch(setData(result.data))
      });
      return next(action);
    default:
      return next(action);
  }
};
```



10. Dans le `reducer`


A. ACTION `GET_DATA`

On va utiliser cette fonction simplement pour déverser le state

- importer l'action `GET_DATA` _(la première action, qu'on utilise pour lancer le tout)_
- créer un CASE
- déverser l'état


B. ACTION `SET_DATA`

- importer l'action creator `SET_DATA` _(la deuxième action qu'on a utilsé pour faire du dispatch)_
- déverser le state
- réasigner la valeur de state _(supposons dans le INITIAL_STATE on `cars`)_ par la nouvelle valeur retournée par le dispatch dans le middleware

```js
// importer les 2 actions
import { GET_DATA, SET_DATA } from 'src/actions';

const INITIAL_STATE = {
  cars: [],
};

const reducer = (state = INITIAL_STATE, action) => {
  switch (action.type) {
    case GET_DATA:
      return {
        ...state,
      };
    case SET_DATA:
      return {
        ...state,
        // le mot data ici est celui qui est déclaré dans la fonction setData en paramètre
        cars: action.data,
      };
    default:
      return state;
  }
};

export default reducer;
```