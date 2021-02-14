# REDUX avec React

1. `yarn add react-redux`

[Documentation.](https://react-redux.js.org/)

2. `import { createStore } from 'redux';`

3. Créer un dossier `src/containers`

4. Créer un dossier par `components`

5. Dedans, on crée `index.js`

- on importe la fonction `connect` de `react-redux`
- on importe dedans le `component` en question

```js
import { connect } from 'react-redux';
import NbColors from 'src/components/NbColors';

// nbColors est le props qu'attend le container NbColors
const mapStateToProps = (state) => {
  return {
    // TOUT CE QUI EST retourné ici, sera en props de notre component, du coup,
    // on regarde ce qu'on a en props de notre component, et on les return ici
    // donc on le lui donne ici, le props
    nbColors: state.nbColors
  };
};

const mapDispatchToProps = {};

// fonction closure : fonction qui renvoie une fonction
// on connecte le composant NbColors au Store
export default connect(
  // on prépare ces 2 fonctions
  mapStateToProps,
  mapDispatchToProps,
  // pour les appliquer à ce component / composant
)(NbColors);
```

6. Du coup, on va aller chercher le component `NbColors` DANS le componenetPARENT DEPUIS ce dossier de containers (et non directement depuis le componentCHILD)

- le cheminement : 
    - on crée nos components CHILD
    - on les récupère dans nos containers _(qui va le transformer)_, en donnant les props
    - on récupère dans le component PARENT le component CHILD à partir de justement ce containers !


7. Pour le `dispatch()`, et on fait le dispatch() quand on veut avoir accès au `action`, donc quand il y a un changement / action qui se passe  car l'autre _(state)_ est juste CONSULTATIF :

- on importe les fontions qu'on va utiliser dans le `dispatch()` _(pas obligé que ce soit des fonctions, on aurait pu avoir un simple props aussi)_
- voilà à quoi va ressembler le dispatch :

```js
import { connect } from 'react-redux';
import NbColors from 'src/components/NbColors';

// nbColors est le props qu'attend le container NbColors
const mapStateToProps = (state) => {
  return {
    // TOUT CE QUI EST retourné ici, sera en props de notre component, du coup,
    // on regarde ce qu'on a en props de notre component, et on les return ici
    // donc on le lui donne ici, le props
    nbColors: state.nbColors
  };
};

// voici le dispatch
// on déclare en paramètre dispatch qu'on va utiliser dans nos fonctions plus bas
const mapDispatchToProps = (dispatch) => ({
  // dispatching plain actions
  // on commence par déclarer le props et en fonction dispatch() on donne la valeur de ce props
  randomizeFirstColor: () => dispatch(setFirstColor(randomHexColor())),
  randomizeLastColor: () => dispatch(setLastColor(randomHexColor())),
  randomizeAllColor: () => {
    dispatch(setFirstColor(randomHexColor()));
    dispatch(setLastColor(randomHexColor()));
  },
});

// fonction closure : fonction qui renvoie une fonction
// on connecte le composant NbColors au Store
export default connect(
  // on prépare ces 2 fonctions
  mapStateToProps,
  mapDispatchToProps,
  // pour les appliquer à ce component / composant
)(NbColors);
```


8. Les props en dure d'un component lors d'un dispatch()

```js
// les ownProps representent les props du component qui sont en durs, 
// qui ne sont donc pas dans le state mais SEULEMENT dans le componenent
// du coup, ils sont dispos dans le second paramètre de la fonction en tant que ownProps
const mapDispatchToProps = (dispatch, ownProps) => ({
  // dispatching plain actions
  // on commence par déclarer le props et en fonction dispatch() on donne la valeur de ce props
  randomizeFirstColor: () => dispatch(setFirstColor(randomHexColor())),
  // du coup, on récupère dans les ownProps la direction
  changeDirection: () => dispatch(setDirectionTo(ownProps.direction)),
});
```