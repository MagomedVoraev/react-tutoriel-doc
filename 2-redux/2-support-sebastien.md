# Redux c'est quoi ?

Passer des props de composants en composants c'est trés énervant et source d'erreur. Le code va vite devnir illisible pour le composant au plus au haut niveau ( celui qui détient toutes les données ).

L'idée de Redux, c'est de déporter l'état de notre application en dehors de nos composants React.

![With Store](./docs/with-store.png)

## C'est bien beau mais techniquement ?

Les méthodes les plus utiles de notre store sont les suivantes : 

- **store.getState()**  : Pour venir récupérer notre state, on demande au store d'aller nous chercher les données dans son entrepôt perso
- **store.dispatch(action)**  : Pour dispatcher une action cad, générer un nouveau state en donnant l'action au listener.
- **store.subscribe(func)**  : pour s'abonner aux changements du state, cad, les callbacks seront exécutés aprés les modifications du state

## Quelles sont les étapes ?

![Flow Redux](./docs/flow.svg)

- On pars d'un premier rendu, on décide de **déclencher une action**, par exemple on demande de changer de couleur.
- On va donc utiliser le **dispatch** avec un **action** en paramètre
- Cette action va partir jusqu'au **reducer** qui est le traducteur d'intention, il va traduire une action en un nouveau **state**
- Ce reducer n'est pas limité à une seule action, il faut donc prévoir qu'il peut y envoir plusieurs qui passent par lui
- On interprète l'action et on renvoie un **nouvel** état, on ne modifie pas l'ancien. On garde l'immutabilité
- Le store détecte donc que son **state** a changé, il va donc choisir de prévenir tout ceux qui étaient **subscribe** à lui. Il va donc executer tout les callbacks qu'il a gardé.

La boucle est bouclée on peut re-déclencher un nouveau dispatch

## Les actions

Une action c'est une intention, on veut faire quelque chose, mais on se moque de comment ça va se faire. Le but c'est juste de le faire.

Une action ça ressemble à ça :

```js
{
    type: 'SET_FIRST_COLOR',
    color: '#FF00FF' // <-- Payload
}
```

La représentation d'une action c'est un objet avec par convention une clef `type` qui a pour valeur un texte en **majuscule** et en **snake case**. Il est possible de rajouter des paramètres en plus qu'on va appeler **payload**, comme ici la couleur `color`

### Action creator

Pour éviter les répétitions et les erreurs de saisies, et profiter de l'auto-complétion on va définir des actions dans un fichier à pars. En déclarant les types dans des constantes et les actions dans des fonction qui vont les créer. Ce sont des `actions creators`

Exemple: 
```js
// Le Type
export const MON_ACTION_SUPER_COOL = 'MON_ACTION_SUPER_COOL';

// L'action creator
export const monActionSuperCool = (payload) => ({
    type: MON_ACTION_SUPER_COOL,
    payload: payload
})

```
