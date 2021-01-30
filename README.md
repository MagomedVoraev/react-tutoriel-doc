# React

## Componenent

Les components representent toutes les parties que composent une app.

### Où sont les components dans notre projet

Les componenents sont créées par `dossiers` dans `src` => `components` => `Componenent1` => `Componenent2` => `Componenent3`..., Sachant qu'il y a déjà par défaut le componenet `App` de base dans notre projet.

### Que se trouve dans le dossier `Component` ?

- les images qui vont y être utilisées
- un fichier `index.js`
- un fichier `style.scss`


#### Que se trouve dans chacun des fichiers

1. Dans le fichier `index.js` :

    ```js
    import React from 'react';

    import './style.scss';


    const Component1 = () => (
        <div>Contenu de mon Component</div>
    );

    // ceci est l'équivalent plus rapide de :
    // const Component1 = () => {
    //    return (
    //        <div>Contenu de mon Component</div>
    //    )
    // }

    export default Component;
    ```

2. Dans le fichier `style.scss`

Dans ce fichier, on va importer le fichier `vars.scss` qui se trouve dans `src/styles` et qui contient toutes les variables que nous avons déclarés.

Puis, on leur donne un alias de `v` _(PAS OBLIGATOIRE)_ afin de faciliter / accélerer l'écriture, et pouvoir écrire `v.$color` au lieu de `vars.$color` par exemple.

    ```scss
    // on importe nos vars qui se trouvent 
    @use 'src/styles/vars' as v;

    // ici, nous écrivons nos 
    ```

### `propTypes`
### `defaultProps`
### `State``

#### `constructor`
#### `setState`
#### `currying`
#### `fonction closure` ou `closure` (une fonction qui retourne une fonction)

### `spread operator`
`...`

## Babel 
## SASS
## MISE EN PLACE PROJET