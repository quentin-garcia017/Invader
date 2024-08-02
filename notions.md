# Notions découvertes ou redécouvertes ce jour

## JS 

```js
// On pourrait si on veut, générer des ids à partir du numéro de colonne et numéro de celulle
newCell.id = `cell-${row}-${cell}`;
// égale à :
newCell.id = "cell-" + row + "-" + cell;
```

```js
// On ajoute un écouteur d'évènement sur ma celulle
// le deuxième paramètre ici, qui est une fonction anonyme s'appelle aussi une fonction de callback
newCell.addEventListener('click', function(event) {
    console.log(event)
});
```

```js
// Grace à element.classList.contains() on a la possibilité de savoir si une classe est présente sur un élément
if(cell.classList.contains('cell--black')) {
    cell.classList.remove('cell--black');
} else {
    cell.classList.add('cell--black');
}

// Attention, meme si c'est cool, ce code est simplifiable en : 
cell.classList.toggle('cell--black');
```

```js
// Pour modifier le contenu d'un élément on peut utiliser
// source : https://stackoverflow.com/questions/35213147/difference-between-textcontent-vs-innertext
element.innerHTML = "Valider"; // plutot à utiliser si on veut définir le html d'un élément mais c'est a éviter, on l'utilise surtout pour VIDER le html : element.innerHTML = "";
element.innerText = "Valider"; // comparable à textContent mais semble prendre plus de perf que lui
element.textContent = "Valider"; // celui a préferer pour changer le text d'un élément
```

### Dataset

Dataset permet de définir coté html un attribut spécial `data-nom="valeur"` (ou nom est-ce que vous voulez)
et de récupérer coté JS cette valeur via `monElement.dataset.nom`

```html
<button class="color color--black" data-color="black" data-coucou="truc" data-toto="42"></button>
```

```js
const button = document.querySelector('button');

button.addEventListener('click', function(event) {
  console.log(event.target.dataset.color);
  console.log(event.target.dataset.coucou);
  console.log(event.target.dataset.toto);
});
```

### Sélectionner pleins d'éléments html d'un coup

Avec ce html 
```html
<button class="color color--black" data-color="black"></button>
<button class="color color--black" data-color="green"></button>
<button class="color color--black" data-color="red" ></button>
```

Disons qu'on veut récupérer ces éléments et ajouter un eventListener sur chaque. On peut faire comme ça : 
```js
// On les récupères tous avec querySelectorAll(), ce qui nous les met dans un tableau
const colorButtons = document.querySelectorAll('.color');

// On les parcours un à un pour leur ajouter un évènement et dedans, récupérer la valeur de chaque data-color
for(button of buttons) {
  button.addEventListener('click', function(event) {
    console.log(event.target.dataset.color);
  });
}
```

## CSS

Les variables css
```css

/* :root représente notre élément racine de la page (html en soit) */
:root {
    /* 
        on défini des variables en utilise le nommage --nom-variable: valeur
        on peut y stocker n'importe quelle valeur de propriété CSS classique
    */
    --color-primary: #9b68e4;
    --color-primary-dark: #3148ad;
    --gap: 4px;
}

body {
    background: var(--color-primary);
}

button {
    /* on l'utilise avec le mot clé var() dans lequel on fourni le nom de la variable définie dans :root */
    background: var(--color-primary);
    color: var(--color-primary-dark);
}

.flex-element {
    display: flex;
    gap: var(--gap);
}
```
