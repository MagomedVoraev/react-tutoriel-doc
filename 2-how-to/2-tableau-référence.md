

[CF: vidéo 2 explication de Vincent, à 1H09](https://drive.google.com/drive/folders/1LwWrmglHMPDdfp0vfk-Z0uLmNtvWLEZX)
```js
const fruits = ['pomme', 'fraise'];

// ici, quand je fais ça, ce que ça va faire c'est que ça va copier
// la référence de fruits dans panier, et donc quand je vais 
// modifier panier par exemple on y push un autre élément, ça 
// va le rajouter dans fruits aussi, mais ON NE VEUT PAS ÇA
const panier = fruits;

// DU COUP, pour éviter ça, on déverse ce qu'il y a dans fruits à panier2
const panier2 = [...fruits];
// donc là, MEME SI je push ou modifie panier2, rien ne sera
// modifié dans fruits


```