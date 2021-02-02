# Le router de React


## Mettre en place un router de la NAV

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


## Mettre en place une route de PARENT => CHILD

[React Router - PARAMS](https://reactrouter.com/web/example/url-params)

1. Dans le `MainComponent`, créer une `<Route></Route>` (**avant la 404**) et mettre le component child qu'on veut créer pour y être redirigé _(ne pas oublier de l'importer)_ et y déclarer le path comme attribut = `path="/article/:id"`

```js
<Route path="/article/:id">
// ici, il faut mettre le childComponentName qui doit être renvoyé
</Route>
```

2. Créer ce childComponentName justement et le préparer

```js
import React from 'react'
import { useParams } from 'react-router-dom';

import './childComponentName.scss';

const childComponentName = () => {
  return (
    <div>
      <h2>Titre</h2>
    </div>
  )
}

export default childComponentName;
```


3. Importer ce childComponent dans notre `mainComponent` + le mettre dans les balises JSX `Routes`

```js
<Route path="/:id">
  <childComponentName />
</Route>
```

4. Dans le `index.js` de `childComponentName`, utiliser les params, pour cela 2 étapes :
 - `import { useParams } from 'react-router-dom';`
 - et dans la fonction childComponentName : `const {id} = useParams();`
 - pour tester : 
    - `console.log(id);`
    - on peut aller dans l'url et taper par exemple : `/8` à la fin du `localhost...` et voir si ça ressort bien en log

5. Maintenant que ça marche, aller dans `mainComponent` et envoyer la data / posts _(dans lequel on a fait axios, récupération des données)_ et les envoyers en `props` à travers `childComponentName` attribut :

```js
<Route path="/:id">
  <childComponentName posts={posts}/>
</Route>
```

6. Aller dans `childComponentName` et récupérer ces données _(qui sont un objet)_ via les props de la fonction globale :

```js
// posts en props afin de les récupérer
const childComponentName = ({posts}) => {}
```

7. Puis, on récupère **LE post** qu'on souhaite avec son `id` avec utilisation de la fonction `find` :

```js
const ArticleDetails = ({ posts }) => {
  const { id } = useParams();

  // ici, on cherche celui qui a un post.id qui est égal à id params entré dans le navigateur
  const foundPost = posts.find((post) => parseInt(post.id, 10) === parseInt(id, 10));
  console.log(id, foundPost)
  
  return (
    <div className="singlePage">
      // on renvoie le title du post trouvé
      <h2 className="singlePage__title">Titre : {foundPost.title}</h2>
    </div>
  )
}
```

8. Mais on peut aussi mettre une condition si jamais il n'a pas retrouvé, ce qui est une gestion des erreurs et une bonne chose à faire :

**(+ code final)**
```js
import React from 'react'
import { useParams } from 'react-router-dom';


import './articleDetails.scss';

const ArticleDetails = ({ posts }) => {
  const { id } = useParams();

  const foundPost = posts.find((post) => parseInt(post.id, 10) === parseInt(id, 10));
  console.log(id, foundPost)
  if (!foundPost) return (<h1 className="singlePage__title">Cet article n'existe pas </h1>)
  else {
    return (
      <div className="singlePage">
        <h2 className="singlePage__title">Titre : {foundPost.title}</h2>
      </div>
    )
  }
}

export default ArticleDetails;
```
