# Utilisation de Sass 

## Installer Sass avec Node.js

### npm install -g sass

## Vérifier la version 

### sass --version

## Compiler un fichier Sass en Css

### sass styles/main.scss styles/main.css

## Compiler un fichier Sass en Css et voir les modifications en temps réel

### sass --watch styles/main.scss:styles/main.css


## Partials et Imports

### Nommer les fichiers qui vont ensuite être importés avec un _ devant : _exemple.scss
### Dans le main.scss : @use "exemple.scss"