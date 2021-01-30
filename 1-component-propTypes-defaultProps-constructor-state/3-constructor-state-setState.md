# Constructor / State / SetState


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