# Récap des notions : saison 3 - JS

Sur cette fiche, vous trouverez un récap (très rapide) des notions qu'on a vu pendant cette saison 3 !

## Épisode 1

- syntaxe JS : comment créer des variables (`let` ou `const`), faire des concaténations, des boucles, des if/else, console.log, etc.
- inclusion fichier JS : avec `<script src="chemin/vers/script.js"></script>` avant la fin du body dans notre HTML !
- fonctions en JS :

  ```javascript
  // déclarer une fonction :
  function maFonction(param1, param2) 
  { 
    // console.log permet d'afficher des messages dans la console du navigateur
    console.log('hello world !');

    // exemple de concaténation
    console.log(param1 + param2);

    return 'ok !';
  }

  // appel de la fonction
  const valeurRetour = maFonction('hello ', 'world !');
  ```

  De la doc si besoin :
  
  - [let](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Statements/let)
  - [const](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Statements/const)
  - [fonctions](https://developer.mozilla.org/fr/docs/Web/JavaScript/Guide/Functions)

## Épisode 2

- DOM : le DOM est une représentation du document HTML, il fait l'**interface entre HTML & JS**
- sélecteurs : on peut récupérer/sélectionner des éléments HTML avec :
  - `getElementById('id_element')` : permet de sélectionner un élément par son id
  - `getElementsByClassName('class_elements')` : permet de sélectionner plusieurs éléments par leur classe (attention, retourne un tableau d'éléments)
  - `querySelector('selecteur_css')` : permet de sélectionner le premier élément trouvé correspondant à un sélecteur CSS
  - `querySelectorAll('selecteur_css')` : permet de sélectionner plusieurs éléments qui correspondent à un sélecteur CSS

  Exemple :

  ```html
  <p id="id-test"></p>
  <div class="class-test">
    <p></p>
  </div>
  <div class="class-test">
    <p></p>
  </div>
  ```

  ```javascript
  document.getElementById('id-test'); // retourne l'élément <p id="id-test></p>
  document.getElementsByClassName('class-test'); // retourne un tableau contenant tous les <div class="class-test"></div>
  document.querySelector('#id-test'); // retourne l'élément <p id="id-test></p>
  document.querySelector('div.class-test p'); // retourne le <p></p> dans le premier <div class="class-test"></div>
  document.querySelectorAll('div.class-test p'); // retourne tous les <p></p> dans les <div class="class-test"></div>
  ```

- innerHTML & textContent :
  - `element.innerHTML` permet de récupérer ou définir le **contenu HTML** d'un élément
  - `element.textContent` permet de récupérer ou définir le **contenu texte** d'un élément
- modifier l'attribut class :
  - `element.classList` permet de récupérer la liste des classes d'un élément (dans un tableau)
  - `element.classList.add('nouvelle-classe');` pour ajouter une classe à un élément
  - `element.classList.remove('nouvelle-classe');` pour supprimer une classe sur un élément
  - `element.classList.toggle('classe');` pour ajouter ou supprimer une classe
- lire/modifier n'importe quel attribut :
  - `element.attributes` permet de récupérer la liste des attributs d'un élément (dans un tableau)
  - `element.setAttribute('nom-attribut', 'valeur');` pour ajouter un attribut à un élément
  - `element.getAttribute('nom-attribut');` pour récupérer la valeur d'un attribut

Quelques liens vers la doc MDN :

- [Intro sur le DOM](https://developer.mozilla.org/fr/docs/Web/API/Document_Object_Model/Introduction)
- [Glossaire sur le DOM](https://developer.mozilla.org/fr/docs/Glossary/DOM)
- [Référence du DOM](https://developer.mozilla.org/fr/docs/Web/API/Document_Object_Model)
- [getElementById](https://developer.mozilla.org/fr/docs/Web/API/Document/getElementById)
- [getElementsByName](https://developer.mozilla.org/fr/docs/Web/API/Document/getElementsByName)
- [querySelector](https://developer.mozilla.org/fr/docs/Web/API/Document/querySelector)
- [querySelectorAll](https://developer.mozilla.org/fr/docs/Web/API/Document/querySelectorAll)
- [Sélecteurs CSS](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Selectors)
- [innerHTML](https://developer.mozilla.org/fr/docs/Web/API/Element/innerHTML)
- [textContent](https://developer.mozilla.org/fr/docs/Web/API/Node/textContent)
- [classList](https://developer.mozilla.org/fr/docs/Web/API/Element/classList)
- [attributes](https://developer.mozilla.org/fr/docs/Web/API/Element/attributes)
- [setAttribute](https://developer.mozilla.org/fr/docs/Web/API/Element/setAttribute)
- [getAttribute](https://developer.mozilla.org/fr/docs/Web/API/Element/getAttribute)

## Épisode 3

- Événements : un évènement est une action de l'utilisateur sur notre page, par exemple un clic sur un bouton, la soumission d'un formulaire, le changement du contenu d'un champ, etc. Toutes ces actions peuvent être détectées depuis JavaScript.
  - addEventListener :

    Pour "écouter" / surveiller un event, on va utiliser un event listener
    ``addEventListener` : la "meilleure" façon de faire

    Pour récupérer la cible de notre événement :
    `const myButton = document.querySelector('#button');`

    On y attache un eventListener :
    ! Attention, ne pas mettre () sur notre event handler !
    `myButton.addEventListener('click', handleClick);`

  - event handlers :

    **Ce qu'on va effectuer quand un event est détecté** : une fonction ! On appelle cette fonction un handler, ou **event handler** ! (to handle = gérer, c'est la fonction qui va gérer notre event)

    Par convention, ces fonctions commençent par handle :

    ```javascript
    function handleClick(event) {
      console.log(event.target); // event.target c'est la cible (élément HTML) sur laquelle on a réelement cliqué

      console.log(event.currentTarget); // currentTarget c'est l'élément HTML sur lequel on a attaché notre écouteur d'événement (eventListener).
    }
    ```

- Interception de la soumission d'un formulaire :

  On écoute pour cela l'évènement `submit` au lieu de l'évènement `click`.
  Il faut aussi qu'on **bloque le comportement par défaut du formulaire**, qui va normalement actualiser la page. Pour cela, on utilise `event.preventDefault();` à l'intérieur de notre event Handler.

  ```javascript
  const myForm = document.getElementById('form-id');
  myFrom.addEventListener('submit', handleFormSubmit);

  function handleFormSubmit(event) {
    // on bloque le comportement par défaut du formulaire
    event.preventDefault();

    // etc. (on met après ce qu'on veut faire quand l'utiliseur soumet le formulaire)
  }
  ```

- ajouter des éléments dans le DOM :
  - avec innerHTML (vu la veille)
  - avec createElement() puis append() / appendChild() / prepend() :

    ```html
    <div id="div-test"></div>
    ```

    Pour ajouter un paragraphe dans ce div, nous pouvons utiliser innerHTML, mais aussi createElement() et append() !

    ```javascript
    const myDiv = document.querySelector('#div-test');

    // on créé le nouvel élément <p></p>
    const newP = document.createElement('p');
    // on peut ajouter du contenu dans ce <p></p>
    newP.textContent = 'coucou';
    // et enfin on l'ajoute au <div></div>
    myDiv.append(newP);
    ```

- les datasets : le mieux c'est de lire [la doc](https://developer.mozilla.org/fr/docs/Learn/HTML/Howto/Use_data_attributes) !

Plus d'infos :

- [addEventListener](https://developer.mozilla.org/fr/docs/Web/API/EventTarget/addEventListener)
- [Intro aux events](https://developer.mozilla.org/fr/docs/Learn/JavaScript/Building_blocks/Events)
- [Référence des évèvenements](https://developer.mozilla.org/fr/docs/Web/Events)
- [createElement](https://developer.mozilla.org/fr/docs/Web/API/Document/createElement)
- [append](https://developer.mozilla.org/en-US/docs/Web/API/Element/append)
- [appendChild](https://developer.mozilla.org/fr/docs/Web/API/Node/appendChild)
- [prepend](https://developer.mozilla.org/en-US/docs/Web/API/Element/prepend)
- [preventDefault](https://developer.mozilla.org/fr/docs/Web/API/Event/preventDefault)

## Épisode 5

- Maintenance du code : organiser son code en plusieurs "modules"

    Un module est un tableau associatif, on peut donc créer un module en suivant l'exemple suivant. Les modules sont une bonne façon de "ranger" notre code JS, en regroupant dans un même module toutes les variables et fonctions qui ont une même "thématique".

    ```javascript
    // création d'un module "test"
    const test = {

        // ajout d'une propriété, une variable dans un module
        // attention, on utilise : et pas = ici, on est dans un tableau associatif !
        str: 'Hello world !',
        str2: 'test,

        // ajout d'une méthode, une fonction dans un module
        // attention, la syntaxe est différente de celle qu'on utilise habituellement pour les fonctions !
        init: function(myStr1, myStr2) {
            // on créé TOUJOURS une méthode init, pour initialiser notre module. 
            // on l'appelera avant d'appeler les autres méthodes de notre module.

            // on initialise dans init la valeur des propriétés du module
            test.str = myStr1;
            test.str2 = myStr2;

            // comme on le voit ci-dessus, pour accéder à une propriété ou une méthode d'un module, 
            // on utilise nom_module.nom_propriété ou nom_module.nom_méthode()
        },

        testMethode: function() {
            // on peut aussi remarquer que les propriétés et méthodes sont séparées par des virgules
            // dans un module.
        }
    };
    ```

- **méthode : fonction dans un module**
- **propriété : variable dans un module**

## Épisode 6

- Cookies
  - Principe :

    Les cookies permettent de stocker des données dans le navigateur de l'utilisateur. Ils sont stockés coté client (dans le navigateur) mais sont aussi accessibles coté serveur (en PHP par exemple).

  - Utilisation :

    - **créer un cookie** :

      Pour créer un cookie, on utilise `document.cookie = 'nom_cookie=valeur_cookie; max-age=nb_secondes_avant_suppr; secure'`

    - **lire un cookie** :

      Pour lire tous les cookies, on utilise `document.cookie` (retourne une chaine de caractères contenant tous les cookies séparés par des ';')

      Pour lire/accéder à la valeur d'un cookie spécifique en fonction de son nom, on utilise `document.cookie.split('; ').find(row => row.startsWith('nom_cookie=')).split('=')[1];`

    - **supprimer un cookie** :

      Pour supprimer un cookie, il faut mettre à jour sa propriété max-age, en la mettant à 0 le cookie s'auto-détruira !
      `document.cookie = 'nom_cookie=; max-age=0; secure';`

    Plus d'informations sur les cookies sur la [doc MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie)

- split() :

  split() permet de découper une chaîne de caractères en fonction d'un motif. Les différentes parties de la chaîne seront stockées dans un tableau (et on pourra y accéder avec []).
  Exemple :

  ```javascript
  str = "Hello world !";
  console.log(str.split(' ')); // affiche ['Hello', 'world', '!']
  console.log(str.split(' ')[0]); // affiche 'Hello'
  ```

  Plus d'infos sur split() sur la [doc MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/String/split)

- LocalStorage :
  - principe :

  Le LocalStorage est un espace de stockage coté client (dans le navigateur), qui nous permet de stocker des données ! (un peu comme les cookies)

  - utilisation :
    - ajouter dans le localStorage : ```localStorage.setItem('clé', 'valeur');```
    - lire quelque-chose dans le localStorage : ```let str = localStorage.getItem('clé');```
    - supprimer quelque chose dans le localStorage : ```localStorage.removeItem('clé');```

    Plus d'infos sur le localStorage sur la [doc MDN](https://developer.mozilla.org/fr/docs/Web/API/Window/localStorage)

- JSON : Le JSON est permet de stocker des données textuelles structurées. C'est un vaste sujet, je vous conseille donc un peu de lecture :
  - [wikipédia](https://fr.wikipedia.org/wiki/JavaScript_Object_Notation)
  - [doc MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/JSON)
  - [tuto JSON sur MDN](https://developer.mozilla.org/fr/docs/Learn/JavaScript/Objects/JSON)

  Il faut retenir qu'on peut **parser** du JSON avec ```let json_data = JSON.parse(json)``` et en créer avec ```let json = JSON.stringify(data)```.
