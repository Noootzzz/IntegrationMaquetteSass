# Utilisation de Sass 

## Installer Sass avec Node.js

``` 
npm install -g sass
``` 

## Vérifier la version 

``` 
sass --version
``` 

## Compiler un fichier Sass en Css

``` 
sass styles/main.scss styles/main.css
``` 

## Compiler un fichier Sass en Css et voir les modifications en temps réel

``` 
sass --watch styles/main.scss:styles/main.css
``` 

## Partials et Imports

### Nommer les fichiers qui vont ensuite être importés avec un _ devant : _exemple.scss
### Pour les importer dans le main.scss : 
``` 
// main.scss

@use "variables.scss";
``` 

## Variables

### Ecriture dans le _variables.scss : 
``` 
// _variables.scss

$background-color: red;
``` 

### Dans le main.scss :  (Le "variables" devant la variable est nécessaire ou non en fonction de la version de Sass.)
``` 
// main.scss

@use "variables.scss";

body {
    background-color: variables.$background-color;
}
``` 

## Imbrication

``` 
// main.scss

nav {
    display: flex;

    ul {
        list_style: none;
    }
}
```

## Méthodologie BEM 

### Elle divise un composants comme par exemple une simple card en 3 éléments :
### - Block (card)
```
// index.html

<div class="card"></div>

// main.scss

.card {
    background-color: red;
}
```
### - Element (card__title, card__description) :
```
// index.html

<div class="card">
    <h2 class="card__title">Titre de la carte</h2>
    <p class="card__description">Description de la carte</p>
</div>

// main.scss

.card {
    background-color: red;

    &__title {
        color: black;
    }
    &__description {
        color: gray;
    }
}
```
### - Modifier du block (card--red) ou d'un element (card__title--large) :
```
// index.html

<div class="card card--blue">
    <h2 class="card__title card__title--large">Titre de la carte</h2>
    <p class="card__description">Description de la carte</p>
</div>

// main.scss

.card {
    background-color: red;

    &__title {
        color: black;

        &--large {
            font-size: 2em;
        }
    }
    &__description {
        color: gray;
    }

    &--blue {
        color: blue;
    }
}
```

## Mixins

### Les mixins permettent de créer des blocs de code réutilisables et paramétrables :

```
// _mixins.scss

@mixin primary-button($radius, $color) {
    border-radius: $radius;
    background-color: blue;
    color: $color;
    padding: 1rem 2rem;
}

// main.scss

@use "mixins.scss";

.button {
    @include mixins.primary-button(8px, #fff);
}
```

## Condition

### Les conditions permettent de changer des elements en fonction d'autres paramètres : 

```
// _variables.scss

@use "sass:color";

$white: #FFFFFF;
$black: #021526;
$blue: #0360D9;

$element-color: if(color.channel($blue, "lightness", $space: hsl) > 50%, $black, $white);
```

## Extend

### L'extend permet de partager des règles entre plusieurs selecteurs :

```
// main.scss

.message {
    padding: 2rem;
    border: 1px solid #fff;
}

.success {
    @extend .message;
    color: green;
}
```

## Boucles

### Les boucles servent à générer dynamiquement du CSS, surtout pour des éléments répétitifs ou des variations de style.

### Boucle for :
```
// Générer des largeurs qui augmentent pour .col-1 à .col-12

@for $i from 1 through 12 {
  .col-#{$i} {
    width: (100% / 12) * $i;
  }
}
```

### Boucle Each : 
```
// Utiliser des couleurs à partir d'une liste de couleurs pour créer des boutons

$colors: (primary: #3498db, success: #2ecc71, danger: #e74c3c);

@each $name, $color in $colors {
  .btn-#{$name} {
    background-color: $color;
    color: white;
    padding: 10px 15px;
    border-radius: 5px;
  }
}
```

### Boucle while :
```
// Générer des marges qui augmentent pour .margin-1 à .margin-5

$i: 1;

@while $i <= 5 {
  .margin-#{$i} {
    margin: $i * 10px;
  }
  $i: $i + 1;
}
```