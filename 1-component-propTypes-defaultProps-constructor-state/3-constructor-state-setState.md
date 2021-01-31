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

## `state`




## `setState`




## Conclusion : constructor, state, setState

Il y a donc ces étapes à suivre pour passer avoir une donnée dynamique sur notre page, et à chaque fois que la donnée change, il est `render` et donc le component s'actualise.

1. `constructor`

On crée le `constructor` en transformant notre fonction en `class` et en l'extendant de `Component` qu'on importe depuis React. On ajoute dans ce `constructor` le `super()`.



2. `this.state`

On déclare un `state` par défaut pour notre futur donnée dynamique.

C'est un objet dans lequel on met nos props afin qu'ils soient gardés / enregistrés :

```js
constructor(props) {
  super(props)

  this.state = {
    // on itilialise la donnée
    count: 0,
  }
}
```


3. Event handler

On donne une fonction à exécuter sur un button par exemple qui `onClick` va enclancher la fonction `changeMessage()` qui aura pour message de changer le text de mon élément 


4. Coder la fonction `changeMessage()`


5. `setState`

On utilise le `setState` pour pouvoir justement changer + `rerender` nos données _(enregistrés dans l'objet this.state = {})_ sur notre navigateur. A chaque fois que la donnée va changer, le component sera RErender. 

```js


```


6. Changement de donnée et donc re `render` du component