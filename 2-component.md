# Component
Les components representent toutes les parties que composent une app.

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


## `propTypes`
On doit définir le **type de propriété** pour chacune des **propriétés / props** d'une fonction.

Supposons, dans notre `Componenet2`, on a la fonction suivante :

 - on commence par importer les `PropTypes`
 - on déclare les props du `Compoment2`

    ```js
    // importation des props
    import PropTypes from 'prop-types';

    const Component2 = () => (
        <div>
            // on suppose qu'on a pleins de props ici pour la fonction pour pouvoir faire le PropTypes
        </div>
    )

    // on déclare toutes nos props du Component2
    Component2.propTypes = {
    
    // supposons currencies est un tableau qui contient un objet
    currencies: PropTypes.arrayOf(
        PropTypes.shape({
        name: PropTypes.string.isRequired,
        rate: PropTypes.number.isRequired,
        }),
    ).isRequired,

    // de type string
    search: PropTypes.string,
    // de type number ET EST REQUIS !
    nbCountr: PropTypes.number.isRequired,
    // de type fonction
    onSearch: PropTypes.func,
    // de type boolean
    done: PropTypes.bool,
    // de type symbol
    optionalSymbol: PropTypes.symbol,
    };
    ```

## `defaultProps`

On déclare des valeurs défauts pour nos props, supposons que ma propType `done` est par défaut à `true` alors on le mettra ici.

  ```js
  Component2.defaultProps = {
    setCurrency: () => { },
    onSearch: () => { },
    search: '',
    selectedCurrencyName: null,
    done: 'true';
  };
  ```

## `Constructor`

On se sert du constructor afin d'y mettre le `state`.

Pour pouvoir utiliser le constructor, on doit faire plusieurs choses :
  - importer le component depuis react, on rajoute donc `{ Component }` dans le import React : => `import React, { Component } from 'react';`
  - convertir la fonction en `Class`
    - dans laquelle on aura maintenant un render
        - dans lequel il y aura un return :
    - dans laquelle on aura notre `constructor`

    ```js
    class ComponentName extends Component {

        constructor(props) {
            super(props);
            // State représente l'état du composant, c'est un objet et il doit être immutable

            // Ici on le déclare dans le constructeur afin de l'initialiser à sa valeur initiale
            // C'est ce qu'on apelle l'initialState
            this.state = {
              open: false,
              baseAmount: 1,
              currency: {
                name: 'Australian Dollar',
                rate: 1.665247,
              },
              search: '',
            };
        }


        render() {

            return (
                <div>Mon Contenu</div>
            )
        }
        
    }

    // == Export
    export default ComponentName;
    ```

## `State`
## `setState`

## `fonction closure` ou `closure` (une fonction qui retourne une fonction)
## `currying` (plusieurs fonctions les unes dans les autres, on envoie les arguments à toutes les fonctions en même temps)

## `spread operator`

## `componentDidMount()`
## `componentDidUpdate()`
## `componentWillUnmount()`
