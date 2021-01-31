# Final Code Result


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
      <div className="todoList">
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