# ROUTER

[React Router](https://reactrouter.com/web/guides/quick-start)

## Mise en place Router

1. On doit commencer par importer le module :

`yarn add react-router-dom`

2. Aller dans le fichier `src/index.js`
```js
// importer le BrowserRouter et le renommer en Router
import { BrowserRouter as Router, } from 'react-router-dom';

// mettre notre const = rootReactElement à l'intérieur du Router
const rootReactElement = (
  <Router>
    <Blog />
  </Router>
);
```

3. Changer les balises `<a>` par `<Link>` partout SAUF dans la `<NAV>`

Trouver partout dans notre projet les balises `a` et les remplacer par `Link`
**/!\ NE PAS REMPALCER DANS LA NAV (MENU DE NOTRE PROJET)**

- `import { Link } from 'react-router-dom';`
  
- remplacer `a` par `Link`
  
- mais aussi, dans ces `a`, remplacer `href` par `to`

```js
// on importe Link
import { Link } from 'react-router-dom';
//...
// on remplace a par Link
// on remplace href par to
<Link to={`/recipe/${dynamiqueLien}`} className="card-link">Voir la recette</Link>
```

-----

4. Dans la barre de navigation du projet `nav`
On remplace les `a` par `NavLink`

- `import { NavLink } from 'react-router-dom';`
- remplacer les `a` par `NavLink`
- et y ajouter un nouveau attribut `activeClassName=""` dans lequel on aura le nom de class css qui sera activé lorsqu'on aura cliqué / entré sur ce `tag` _(permet par exemple d'afficher une couleur bleu pour le lien dans lequel on sera)_

```js
// on importe NavLink
import { NavLink } from 'react-router-dom';

// ...

const Menu = ({ recipe }) => (
  <nav className="menu">
    // on remplace a par Navlink
    // on change href par to
    // on ajoute exact
    // on ajoute 'activeClassName'
    <NavLink className="menu-link" to="/" exact activeClassName="menu-link--active">
      Accueil
    </NavLink>

    // la même chose ici, sauf qu'on a une boucle map
    {recipes.map((recipe) => (
      <NavLink
        key={recipe.id}
        className="menu-link"
        activeClassName="menu-link--active"
        exact
        to={`/recipe/${recipe.slug}`}
      >
        {recipe.title}
      </NavLink>
    ))}
  </nav>
);
```

5. Dans le `ParentComponent`, on met en place notre système de `routes`

- `import { Route, Switch } from 'react-router-dom';` *(on peut faire le Redirect aussi si on veut)*

- Mettre entre les balises `<Switch></Switch>` tous les `Components` "dynamiques" OU qui doivent changer / s'afficher / ne pas s'afficher selon des conditions. Par exemple, le header et le footer qui doivent toujours apparaitre ne doivent pas être mis dans la balise `<Switch></Switch>`. Donc on n'y met que les routes conditionnelles.

- A l'intérieur de ce `Switch`, on crée des balises `<Route></Route>`
  - dans cette balise, on aura comme attribut `path=""` et `exact`

- et à l'intérieur de cette balise `<Route></Route>`, on met le `ChildComponent` qui doit être affiché

```js
// on importe Route et Switch
import { Route, Switch, Redirect } from 'react-router-dom';

// ...

const App = () {
  // 
  return (
    <div className="app">
      // le component statique, qui s'affiche quoi qu'il arrive (header)
      <Header recipes={recipes.list} />

      // à partir de là, commencent les routes conditionnelles
      <Switch>
        // pour la route "/" + exact
        <Route path="/" exact>
          // on affichera ce component lors de la route "/"
          <Home recipes={recipes.list} />
        </Route>

        // permet de faire une redirrection
        <Redirect from="/recipies" to="/recipie-all" />

        // la route de l'error, qui est un component qu'on importe, et dans lequel on aura juste un 
        // text qui dit quelque chose du genre 'page erreur'
        // et dans les components, on fera un 'return <Redirect to="/error" />' en cas d'erreur
        <Error />

      </Switch>
    </div>
  );
}
```


## Router + Params `useParams()`

**+ BONUS : PASSAGE DE PARAMS / ROUTE DYNAMIQUE AVEC PARAMS** 

Toujours dans le `mainComponent`...

6. Utilisation de `params`

- On ajoute une balise `<Route></Route>` dans laquelle on ajoute le `component` qu'on veut afficher selon le `params`
- On donne à cette `Route` un attribut `path` dans lequel on aura le chemin + `/../:params`
- On met à l'intérieur de cette balise `<Route></Route>` la childComponent qui doit être affiché sur cette route

```js
// on ajoute le path dans la route avec déclaration des params après les deux points "/:ceciEstParams"
<Route path="/recipe/:recipeName">
    // on met le childComponent qui doit être affiché ici
    <Recipe recipe={recipes.list} />
</Route>
```

7. Dans le childComponent

Afin de pouvoir utiliser ces params

- `import { useParams } from 'react-router-dom;'`

- on déclare ce qui sera le résultat de notre `params` : `const { recipeName } = useParams();`

- on lui associe une valeur : `const matchRecipe = recipe.find((element) => element.slug === recipeName);`

- on l'utilise dans le `return` de notre `childComponent`

```js
// ...

import { useParams } from 'react-router-dom';
// ...

const Recipe = ({ recipe }) => {
  // déclaration des params
  const { recipeName } = useParams();
  // recherche de ce qui doit être l'équivalent de mon params par une fonction find
  const matchRecipe = recipe.find((element) => element.slug === recipeName);

return (
    
      <div className="recipe">
        <Ingredients
          // utilisation de params + résultat des recherches
          list={matchRecipe.ingredients}
        />
      </div>
  );
}
```
