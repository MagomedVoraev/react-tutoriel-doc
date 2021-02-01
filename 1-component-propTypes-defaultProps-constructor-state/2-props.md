# Props

Les props sont les propriétés passées en paramètres dans les fonctions.

  - `propTypes`
  - `defaultProps`


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


## Utilisation des props dans le component parent

```js
const ComponentParent = () => {
  return (
    <ComponentEnfant
    // je vais utiliser dedans toutes les props qui ont été déclarées
    search={search}
    currency=1
    />
  )
}

export default ComponentParent;
```

