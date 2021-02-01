# Le router de React

Permet d'afficher ou de cacher les COMPOSANTS, car en vrai, React compile tout notre code en UNE SEULE PAGE !

Donc ce ne sont pas des PAGES qui sont affichées / cachées mais bien des COMPOSANTS / components.


[React Router](https://reactrouter.com/web/guides/quick-start)

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
3. `import { navLink } from 'react-router-dom';`

4. Mettre des balises `NavLink` au lieu de `a` dans nav=>ul=>li

5. Mettre dans cette balise un attribut `to={leLien}` + `activeClassName` que sera détecté automatiquement quand l'utilisateur clique sur le lien (il devient Active) + `exact` pour lui dire qu'il doit regarder EXACTEMENT le lien donné et rien d'autre

6. Créer component 404 : `Erreur404` => `index.js`

```js
import React from 'react';

const Error404 = () => (
  <h1>Erreur page introuvable</h1>
);

export default Error404;
```
**Créer un fichier scss et donner un style à ce component (optionnel)**

7. Importer cette page dans notre main Component `import Erreur404 from 'src/components/Erreur404'`


8. Toujours dans le main Component `index.js`, importer le switch

```js
import {
  Switch,
  Route,
} from 'react-router-dom';
```

9. Toujours dans le même fichier, mettre la balise `Route` dans `Switch`, et on rajoute l'attribut `path="/leLien"` qu'on veut dans le `Route` + `exact` afin qu'il prenne la route EXACTE + `key={}`!

```js
// == Composant
const Blog = () => (
  <div className="blog">
    <Header categories={categoriesData} />
    <Switch>
      {categoriesData.map((category) => (
        <Route path={category.route} exact key={category.route}>
          <Posts posts={postsData} category={category} />
        </Route>
      ))}

      <Route>
        <Erreur404 />
      </Route>
    </Switch>
    <Footer />
  </div>
);

// == Export
export default Blog;
```


10. On peut boucler / `map` afin d'avoir toutes les routes de manière dynamique


```js
// == Composant
const Blog = () => (
  <div className="blog">
    <Header categories={categoriesData} />
    <Switch>
      {categoriesData.map((category) => (
        <Route path={category.route} exact>
          <Posts posts={postsData} category={category} />
        </Route>
      ))}

      <Route>
        <Erreur404 />
      </Route>
    </Switch>
    <Footer />
  </div>
);

// == Export
export default Blog;
```


11. Final Code 

```js
// == Import npm
import React from 'react';
import {
  Switch,
  Route,
} from 'react-router-dom';

// == Import
import Header from 'src/components/Header';
import Posts from 'src/components/Posts';
import Footer from 'src/components/Footer';

import categoriesData from 'src/data/categories';
import postsData from 'src/data/posts';

import Erreur404 from 'src/components/Erreur404';
import './styles.scss';

// == Composant
const Blog = () => (
  <div className="blog">
    <Header categories={categoriesData} />
    <Switch>
      {categoriesData.map((category) => (
        <Route path={category.route} exact key={category.route}>
          <Posts posts={postsData} category={category} />
        </Route>
      ))}

      <Route>
        <Erreur404 />
      </Route>
    </Switch>
    <Footer />
  </div>
);

// == Export
export default Blog;
```



12. Créer un dossier `selectors` dans `src`

=> dedans on crée `ceQuiEstFiltré.js` (ici posts.js)

On va y créer une fonction 
```js
/* eslint-disable import/prefer-default-export */
/**
 * Fonction permettant de filtrer les posts suivant une nom de categorie
 * @param {Array} posts
 * @param {String} categoryLabel
 */
export const getPostsByCategory = (posts, categoryLabel) => {
  if (categoryLabel === 'Accueil') {
    return posts;
  }
  return posts.filter((post) => (post.category === categoryLabel));
};
```


13. On revient dans le mainComponent et on importe cette fonction pour l'utiliser dans le Router

`import { getPostsByCategory } from 'src/selectors/posts';`

```js
// == Composant
const Blog = () => (
  <div className="blog">
    <Header categories={categoriesData} />
    <Switch>
      {categoriesData.map((category) => (
        <Route path={category.route} exact key={category.route}>
          <Posts
            // c'est ici que j'utilise la fonction AVEC les props
            posts={getPostsByCategory(postsData, category.label)}
            categoryLabel={category.label}
          />
        </Route>
      ))}

      <Route>
        <Erreur404 />
      </Route>
    </Switch>
    <Footer />
  </div>
);

// == Export
export default Blog;
```


14. Si on veut `redirect` à une route différente de la route entrée

- importer `Redirect` dans notre `...from 'react-router-dom';`

- on ajoute AVANT la route de 404 :
```js
<Redirect from="/jquery" to="/autre" />
```

final code: 
```js
// == Import npm
import React from 'react';
import {
  Switch,
  Route,
  Redirect,
} from 'react-router-dom';

// == Import
import Header from 'src/components/Header';
import Posts from 'src/components/Posts';
import Footer from 'src/components/Footer';

import categoriesData from 'src/data/categories';
import postsData from 'src/data/posts';

import { getPostsByCategory } from 'src/selectors/posts';

import Erreur404 from 'src/components/Erreur404';
import './styles.scss';

// == Composant
const Blog = () => (
  <div className="blog">
    <Header categories={categoriesData} />
    <Switch>
      {categoriesData.map((category) => (
        <Route path={category.route} exact key={category.route}>
          <Posts
            posts={getPostsByCategory(postsData, category.label)}
            categoryLabel={category.label}
          />
        </Route>
      ))}
      <Redirect from="/jquery" to="/autre" />
      <Route>
        <Erreur404 />
      </Route>
    </Switch>
    <Footer />
  </div>
);

// == Export
export default Blog;

```