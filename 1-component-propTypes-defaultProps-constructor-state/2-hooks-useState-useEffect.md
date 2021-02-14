# Hooks
_Quand on parle de Hook, par convention, on parlde fonction qui commencent par `'use...'`_


## `useState`
[Hook - useState](https://fr.reactjs.org/docs/hooks-state.html)

Use state permet d'utiliser l'équivalent de state et setState sans avoir à faire une class.

```js
const [count, setCount] = useState(0);
// ce code équivaut à dire
// count = 0
// + avec utilisation de la fonction setCount(count + 1)
// c'est l'équivalent de setState mais uniquement pour le count


// UN AUTRE EXEMPLE :
const [loading, setLoading] = useState(false);
```


Utilisation de `&&` (opérateur double et logique)
```js
// == Composant
const Blog = () => {
  const [loading, setLoading] = useState(false);
  return (
    <div className="blog">
      <Header categories={categoriesData} />
      // si loading est TRUE (contraire de false) alors AFFICHE ce qui vient après &&
      {!loading && (
        <Switch>
          {categoriesData.map((category) => (
            <Route path={category.route} exact key={category.route}>
              <Posts
                posts={getPostsByCategory(postsData, category.label)}
                categoryLabel={category.label}
              />
            </Route>
          ))}
          <Redirect from="/jquery" to="/autre" />
          <Route>
            <Erreur404 />
          </Route>
        </Switch>
      )}
      <Footer />
    </div>
  );
};

// == Export
export default Blog;
```


On peut EN PLUS faire un ternaire pour dire SI JE SUIS EN LOADING tu m'affiche toute la structure, SINON `en chargement...`

```js
// == Composant
const Blog = () => {
  const [loading, setLoading] = useState(true);
  return (
    <div className="blog">
      <Header categories={categoriesData} />

      // utilisation du TERNAIRE
      {!loading ? (

        <Switch>
          {categoriesData.map((category) => (
            <Route path={category.route} exact key={category.route}>
              <Posts
                posts={getPostsByCategory(postsData, category.label)}
                categoryLabel={category.label}
              />
            </Route>
          ))}
          <Redirect from="/jquery" to="/autre" />
          <Route>
            <Erreur404 />
          </Route>
        </Switch>

        // ternaire
      ) : 'Chargement cours'}

      <Footer />
    </div>
  );
};

// == Export
export default Blog;
```


## `useEffect`
**_on les voit après avoir vu le cours 7-ajax_**

Récupérer les useEffect depuis React : `import React, { useEffect } from 'react';`


### componentDidMount
Au chargement initial ET lors d'évolutions :
```js
// La fonction de callback en paramètre du useEffect
// va être appellée APRES chaque render
useEffect(() => {
  console.log('Effet de bord de blog');
});
```

### componentDidUpdate
UNIQUEMENT au chargement initial
```js
// 
useEffect(() => {
  console.log('A chaque update');
}, []);
```

UNIQUEMENT si le contenu de la variable `info` change, cet effet sera relancé
```js
// 
useEffect(() => {
  console.log('A chaque update');
}, [info]);
```


### componentWillUnmount
```js
// Ici en deuxième paramètre de useEffect, on met un tableau VIDE
// La première fois qu'on render, useEffect ne peux pas comparer avec sa précédente valeur ( y'en a pas ), donc il execute le callback
// A partir du deuxième render, useEffect peut comparer.
// Sauf qu'il compare les variables à l'intérieure de son tableau ( deuxième paramètre qui en soit est optionnel )
// Si jamais quelque chose évolue à l'interrieur de ce tableau, alors potentiellement le useEffect doit pouvoir changer, donc il rééxecute la fonction de callback
// Sauf que là, le tableau est vide, donc il ne variera jamais.
// Du coups il n'éxécutera la fonction de callback qu'une seule fois, au montage du composant
// Et la fonction de nettoyage, qu'une seule fois aussi, au démontage du composant
// On a donc codé l'equivalent de componentDidMount et componentWillUnmount

// c'est le RETURN en callback qui fait office de nettoyage / unmount
useEffect(() => {
  console.log('Effet de bord de blog');
  return () => {
    console.log('Nettoyage de l\'effet de bord de blog');
  };
}, [info]);
```