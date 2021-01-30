# React

## Componenent

Les components representent toutes les parties que composent une app.

### Dans le Component

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

    // ici, nous écrivons notre code scss
    ```

### `propTypes`
### `defaultProps`

### `constructor`
### `State`
### `setState`

### `fonction closure` ou `closure` (une fonction qui retourne une fonction)
### `currying` (plusieurs fonctions les unes dans les autres, on envoie les arguments à toutes les fonctions en même temps)

### `spread operator`

## Babel 
## SASS
## MISE EN PLACE PROJET