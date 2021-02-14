# Rapatrier la BDD - Data dans le front

- Commencer par installer le package [axios](https://github.com/axios/axios#example): `yarn add axios`

- Modifier fichier .babel de React Model

    - rajouter dans les 'presets' de babel dans un tableau (on doit avoir tout ça) :

    ```js
    {
        "presets": [
            ["@babel/preset-env", {
            "useBuiltIns": "usage",
            "corejs": 3
            }],
            "@babel/preset-react"
        ],
        "plugins": [
            "@babel/plugin-proposal-class-properties",
            "@babel/plugin-proposal-object-rest-spread"
        ]
    }
    ```

- installer `yarn add core-js@3`

- créer un dossier 'commons' dans src/ et dedans crée `api.js`

- `import axios from 'axios'` + CODE avec URL de l'api :

```js
/* eslint-disable import/prefer-default-export */
import axios from 'axios';

export const axiosInstance = axios.create({
  baseURL: 'https://oblog-sarah-maau.herokuapp.com/api',
});
```

- fichier index.js du mainComponent :
    - importer la fonction `axiosInstance`
    - dans la main fonction : 
    ```js
    const [posts, setPosts] = useState([]);

    const loadPosts = async () => {
        try {
            // ce setLoading n'a pas de rapport avec la API,
            // c'est pour afficher le logo de chargement de la page
            setLoading(true);
        // On simule la récupération d'articles

        const response = await axiosInstance.get('/posts');

        // 
        if (response.statusText !== 'OK') {
            throw new Error(`Erreur de requete GET. Erreur ${response.statusText}`);
        }
        // Sinon plus simplement on peut faire comme ça directement
        // const response = await axios.get('https://oblog-sarah-maau.herokuapp.com/api/posts');
        // On part du principes que les posts récupérés sont postsData
        // postsData représente ici ce qu'on a récupéré de l'api
        setPosts(response.data);// Ici on a les posts que si ca s'est bien passé, donc plutot le mettre dans un then
        }
        catch (error) {
            console.log(error);
            alert(error.message);
        }
        // Que cela se soit bien passé ou pas, donc qu'on soit allé à la fin du try ou qu'on soit rentré dans le catch
        // Dans tous les cas on passera dans le finally
        // Du coups le finally est trés pratique pour mettre fin à un loading
        // Car que cela se soit bien passé ou pas, dans tout les cas ça charge plus
        finally {
            setLoading(false); // Pour mettre fin au chargement
        }
    };
    ```

```js
const loadPosts = async () => {
    // Récupération de données
    // ATTENTION : on doit éviter de réécrire l'url à chaque fois, le plus simple serait 
    // de déclarer par exemple : const baseUrl = 'https://oblog-sarah-maau.herokuapp.com/api/posts'
    const response = await axios.get('https://oblog-sarah-maau.herokuapp.com/api/posts');
};
```

- la même chose (mais qui retourne categories au lieu de posts) MAIS AVEC `then` (sans async), _l'un n'est pas meilleur que l'autre_ :

```js
const [categories, setCategories] = useState([{
    route: '/',
    label: 'Accueil',
  }]);

const loadCategories = () => {
    setLoading(true);

    axiosInstance.get('/categories')
      .then((response) => {
        if (response.statusText !== 'OK') {
          throw new Error(`Erreur de requete GET. Erreur ${response.statusText}`);
        }
        return response.data;
      })
      .then((categoriesData) => {
        setCategories(categoriesData);
      })
      .catch((error) => {
        alert(error.message);
      })
      .finally(() => {
        setLoading(false); // Pour mettre fin au chargement
      });
};
```