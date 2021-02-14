# ROUTER

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

3. Changer les balises `<a>` par `<Link>` partout SAUF dans la `<NAV>`

Trouver partout dans notre projet les balises `a` et les remplacer par `Link`
**/!\ NE PAS REMPALCER DANS LA NAV (MENU DE NOTRE PROJET)**

- `import { Link } from 'react-router-dom';`
  
- remplacer `a` par `Link`
  
- mais aussi, dans ces `a`, remplacer `href` par `to`

-----

4. Dans la barre de navigation du projet `nav`
On remplace les `a` par `NavLink`

- `import { NavLink } from 'react-router-dom';`
- remplacer les `a` par `NavLink`
- et y ajouter un nouveau attribut `activeClassName=""` dans lequel on aura le nom de class css qui sera activé lorsqu'on aura cliqué / entré sur ce `tag` _(permet par exemple d'afficher une couleur bleu pour le lien dans lequel on sera)_


5. Dans le `ParentComponent`, on met en place notre système de `routes`

- `import { Route, Switch } from 'react-router-dom';`

- Mettre entre les balises `<Switch></Switch>` tous les `Components` "dynamiques" OU qui doivent changer / s'afficher / ne pas s'afficher selon des conditions. Par exemple, le header et le footer qui doivent toujours apparaitre ne doivent pas être mis dans la balise `<Switch></Switch>`. Donc on n'y met que les routes conditionnelles.

- A l'intérieur