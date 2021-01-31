# Component
Les components representent toutes les parties que composent une app.

- Pour génèrer un component avec emmet : **`rce`**

## Dans le Component
1. Dans le fichier `index.js` :

    ```js
    import React from 'react';

    // on importe les autres components qu'on aura besoin ici
    import Component2 from 'src/component/Component2'

    // On importe les styles
    import './style.scss';


    const Component1 = () => (

        <div>Component1</div>

        // on utilise le component importé
        <Component2 />
    );

    // ceci est l'équivalent plus rapide de :
    // const Component1 = () => {
    //    return (
    //        <div>Contenu de mon Component</div>
    //    )
    // }

    export default Component1;
    ```

2. Dans le fichier `style.scss`

Dans ce fichier, on va importer le fichier `vars.scss` qui se trouve dans `src/styles` et qui contient toutes les variables que nous avons déclarés.

Puis, on leur donne un alias de `v` _(PAS OBLIGATOIRE)_ afin de faciliter / accélerer l'écriture, et pouvoir écrire `v.$color` au lieu de `vars.$color` par exemple.

   ```css
    // on importe nos vars qui se trouvent 
    @use 'src/styles/vars' as v;

    /* ici nous écrivons notre code scss
    exemple
    */
    .toggler {
        position: relative;
        z-index: 1;
        width: 50px;
        height: 50px;
        margin: -25px auto;
        display: block;
        border-radius: 50%;
        background-color: vars.$color-light;
        border: 4px solid vars.$color;
        color: vars.$color;
        font-size: 2em;
        font-weight: bold;
        transition: all vars.$transition-fast;
  
        &:hover { /* .toggler:hover */
            background-color: vars.$color-alt;
        }

        &--open { /* .toggler--open */
            transform: rotate(90deg);
        }
    }
   ```