# Constructor / State / SetState

## `Constructor`

- Pour génèrer le constructor avec emmet : **`rconst`**

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

Le state se déclare dans le constructor sous forme d'un objet.

```js
constructor(props) {
  super(props);

  this.state = {
    // ici je déclare mes props
    // ex :
    message: '',
  }
}
```



## `setState`

Le setState permet de changer les données de mes state déclarées plus haut.

1. Créer la fonction fléchée qui se lance sur l'action de quelque chose _(ex: dans notre render, quand on clique sur un component `onClick=this.changeMessage`)_
2. Destructurer les éléments de `state` qui seront utilisés dans la fonction
3. Utiliser `setState`
4. Changer la valeur de `state`

```js
// 1. créer la fonction fléchée
changeMessage () => {
  // 2. je destructure
  const { message } = this.state;

  // 3. utiliser setState sous forme d'objet
  this.setState({
    // 4. changer la valeur de state
    message: 'voilà, le texte de message a été changé',
  });
}
```



## Conclusion : constructor, state, setState

Il y a donc ces étapes à suivre pour passer avoir une donnée dynamique sur notre page, et à chaque fois que la donnée change, il est `render` et donc le component s'actualise.

1. `constructor`
On crée le `constructor` en transformant notre fonction en `class` et en l'extendant de `Component` qu'on importe depuis React. On ajoute dans ce `constructor` le `super()`.


```js
// avec emmet faire : rconst
constructor(props) {
  super(props);
}
```


2. `this.state`
On déclare un `state` par défaut pour notre futur donnée dynamique.
C'est un objet dans lequel on met nos props afin qu'ils soient gardés / enregistrés :

```js
// avec emmet faire : rconst
constructor(props) {
  super(props)

  this.state = {
    // on itilialise la donnée
    count: 0,
  }
}
```


3. Event handler + **NE PAS OUBLIER DE DESTRUCTURER** LA DONNÉE DYNAMIQUE
On donne une fonction à exécuter sur un button par exemple qui `onClick` va enclancher la fonction `incrementCount()` qui aura pour message de changer le text de mon élément

```js
/// 3. J IMPORTE ET JE DESTRUCTURE LE COUNT, QUI EST UNE DONNÉE DYNAMIQUE QUI VARIE / CHANGE
    const { count } = this.state;
```


6. Le component sera RE-`render` à chaque fois que je clique sur le button et que la value est incrémentée.





## Final result 
```js
// 1. JE TRANSFORME LA FONCTION EN COMPONENT (ON PEUT FAIRE PURECOMPONENT AUSSI)
class TodoList extends PureComponent {
  constructor(props) {
    super(props)

    // 2. J'INITIALISE LE STATE
    this.state = {

      // J'INITIALISE LA DONNÉE
      count: 0,
    }
  }

  // 5. je crée la fonction qui setState count +1 à chaque fois que je clique sur le button
  incrementCount () => {
    const { count } = this.state;

    this.setState = {
      count=+1,
    }
  }

  render() {
    
    // 3. J IMPORTE ET JE DESTRUCTURE LE COUNT, QUI EST UNE DONNÉE DYNAMIQUE QUI VARIE / CHANGE
    const { count } = this.state;

    return (
      <div>
        // 4. JE CRÉE LA FONCTION SUR UN EVENT HANDLER
        <button onClick={this.incrementCount} >
          Incrémentaer
        </button>
      </div>
    );
  }
}

// == Export
export default TodoList;
```