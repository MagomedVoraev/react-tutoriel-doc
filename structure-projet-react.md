# Structure

De ce qui nous intéresse pour coder, voici la structure d'un projet React.

À la racide du projet, on a le dossier `src` dans lequel il y a 4 sous-dossiers :


 - dossier **`assets`** dans lequel on :
    - dossier `fonts`
    - la `favicon.ico` de notre app
    - le fichier `index.html` global, dans lequel on a :

        ```html
        <!DOCTYPE html>
        <html lang="fr">
            <head>
                <meta charset="utf-8" />
                <meta name="viewport" content="width=device-width, initial-scale=1.0" />
                <meta http-equiv="x-ua-compatible" content="ie=edge" />
                <title>Modele</title>
            </head>
            <body>
                <div id="root"></div>
            </body>
        </html>
        ```

 - dossier **`components`** dans lequel on :
    - la liste des components avec première lettre du nom en majuscule, `App`, dans ces components on a :
        - `index.js`
        - `style.scss`

 - dossier **`data`** dans lequel on :
    - un fichier `dataName.js` dans lequel on a toutes les données traitées dans l'app

 - dossier **`styles`** dans lequel on :
    - fichier `_reset.css` avec nos styles reset
    - fichier `_vars.scss` dans lequel on déclare toutes nos vars scss
    - fichier `index.scss` dans lequel :
        ```scss
        @use 'reset';
        @use 'vars';

        @font-face {
            font-family: 'Roboto';
            src: url('../assets/fonts/Roboto-Regular.ttf');
        }

        body {
            font-family: 'Roboto', sans-serif;
            background-color: vars.$color;
        }
        ```

 - fichier global `index.js` dans lequel on a :
    ```js
    // == Import : npm
    import React from 'react';
    import { render } from 'react-dom';

    // == Import : local
    // Composants
    import TodoList from 'src/components/TodoList';

    // == Render
    // 1. Élément React racine (celui qui contient l'ensemble de l'TodoList)
    //    => crée une structure d'objets imbriqués (DOM virtuel)
    // ce nom (TodoList) doit être donné PAR RAPPORT au nom du MAIN component
    const rootReactElement = <TodoList />;

    // 2. La cible du DOM (là où la structure doit prendre vie dans le DOM)
    // c'est le nom qu'on retrouve dans le index.html, donc tout notre code sera dedans, et on le lance
    const target = document.getElementById('root');

    // 3. Déclenchement du rendu de React (virtuel) => DOM (page web)
    render(rootReactElement, target);
    ```