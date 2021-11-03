# currentTarget & target

Quand on travaille avec un évèvenement en JS, on a souvent besoin de récupèrer la "cible" de l'évènement, c'est à dire l'élément HTML (un bouton, par exemple), qui a déclenché cet évèvenement.

## Un petit rappel sur les évènements en JS

Imaginons que nous ayons un bouton dans notre HTML :

```html
<button id="bouton">Cliquez ici !</button>
```

Si on veut y attacher un évènement, on va faire le code JavaScript suivant :

```javascript
// d'abord on récupère le bouton
const myButton = document.getElementById('bouton');

// ensuite on attache notre écouteur d'évènement sur notre bouton
myButton.addEventListener('click', handleClick);
```

Dans le code JS ci-dessus, on commence par récupèrer notre élément HTML (le bouton) avec `getElementById`, et on le stocke dans une variable `myButton`.

Ensuite, on ajoute notre écouteur d'évènement (EventListener en Anglais) avec `addEventListener`, **sur notre bouton**. On passe le type d'évènement que l'on veut "écouter" en premier paramètre (ici `click`), et en deuxième paramètre la fonction qu'on veut appeler quand l'évènement se produit (notre EventHandler, ici `handleClick`).

## Mais la cible, du coup c'est quoi ?

En JavaScript, on a deux "cibles" possibles :

- currentTarget
- target

Ces deux propriétés sont accessibles uniquement à l'intérieur de notre fonction `handleClick`, sur le paramètre `event` :

```javascript
// cette fonction sera appelée quand l'utilisateur va cliquer sur le bouton
function handleClick(event) {

    // ici, on a accès à event.target et event.currentTarget

}
```

Ok, c'est bien beau tout ça, mais je ne sais toujours pas à quoi ça sert, et quelle est la différence entre les deux ...

## La différence

`event.currentTarget`, c'est __l'élément HTML sur lequel on a attaché l'évènement__. Dans notre cas, c'est donc `myButton` ! (remontez un peu, on a bien attaché notre eventListener sur `myButton`)

`event.target`, c'est __l'élément HTML sur lequel l'utilisateur a vraiment cliqué__. Dans notre cas, ce sera aussi `myButton`, mais pas toujours ! On va voir un exemple plus bas pour lequel target ≠ currentTarget.

Pour s'en souvenir et comprendre un peu mieux, il faut imaginer que l'utilisateur est un sniper qui essaye d'assassiner un VIP. L'utilisateur vise et tire sur sa cible, mais il peut arriver que la balle n'atteigne pas vraiment la cible ... et soit par exemple interceptée par un garde du corps !

Dans cette analogie, **le VIP c'est currentTarget**. C'est la cible sur laquelle l'utilisateur a tiré.
**Le garde du corps**, qui peut parfois intercepter la balle, **c'est target**.
La plupart du temps la balle atteindra le VIP, mais des fois l'utilisateur peut tirer sur le garde du corps, même si ce n'est pas lui qu'il visait.

![bodyguard](https://user-images.githubusercontent.com/43950280/120458971-07e7a900-c398-11eb-9954-4a63abb25487.png)

## Un autre exemple

On va voir un exemple dans lequel **target ≠ currentTarget**, notre grille pour la bataille navale !

```html
<div id="grid">
    <div id="cell01"></div>
    <div id="cell02"></div>
    <div id="cell03"></div>
    <!-- etc. -->
</div>
```

Pour savoir sur quelle cellule de la grille l'utilisateur a tiré, on pourrait ajouter autant de eventListener que l'on a de cellules, mais ça risque d'être un peu long ...

La meilleure solution dans ce cas, c'est d'attacher un seul eventListener sur notre grille (id=grid) et **regarder ensuite sur quelle cellule (sur quel garde du corps) l'utilisateur a vraiment cliqué, avec target !**

```javascript
// on récupère la grille
myGrid = document.getElementById('grid');

// on ajoute notre eventListeneur
myGrid.addEventListener('click', handleGridClick);

// et enfin, notre event Handler, handleGridClick :
function handleGridClick(event) {

    // ici, target ≠ currentTarget !
    // vérifions avec un console.log :

    console.log(event.currentTarget.id); 
    // retourne l'id de la currentTarget, l'id de l'élément sur lequel on a attaché notre EventListener.
    // ce sera toujours "grid" donc, puisqu'on a attaché notre EventListener sur myGrid
    // currentTarget, c'est le VIP dans l'analogie du garde du corps.

    console.log(event.target.id);
    // retourne l'id de ce sur quoi l'utilisateur a rééllement cliqué !
    // ça pourra donc être "cell01" si l'utilisateur a cliqué sur la cellule 01, "cell02", "cell03", etc.
    // target, c'est le garde du corps qui s'est mis sur la trajectoire de la balle !
}