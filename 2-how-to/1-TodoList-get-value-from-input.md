# Récupérer le texte d'un input à la soumission du formulaire.

```js
class ComponentName extends Component {

    constructor(props) {
        super(props)

        this.state = {

        }
    }
    
    handleOnSubmit = (event) => {
        alert(`Le nom a été soumis : ${this.state.value}`);
        event.preventDefault();
    }

    render() {

        return (
            <form>
                <label>
                    Nom :
                    <input type="text" onSubmitForm={this.handleChange} />
                </label>
                <input type="submit" value="Envoyer"/>
            </form>
        );
    }
}

```