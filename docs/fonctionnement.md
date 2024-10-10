#Les fonctionnalités en détail

Voici les 3 fonctionnalités principales offertes par FluxCEN


## Le fichier *flux.csv*

Situé à la racine du projet, le fichier ***`flux.csv`*** est le coeur de l'application. C'est lui qui centralise toutes les ressources et permet l'affichage de ces dernières dans le plugin.



## Styles pour les ressources en WFS

Il est possible de gérer les styles des flux WFS directement depuis FluxCEN.

Il faut pour cela :

1. Ouvrir le flux dans QGIS
2. Paramétrer le style et l'enregistrer au format `.qml`
3. Déposer ce fichier .qml nouvellement créé dans le dossier `styles_couches` du plugin
4. Indiquer le nom du fichier dans la colonne *style* du fichier *flux.csv* pour la ressource concernée

A l'ouverture depuis FluxCEN, la couche sera alors chargée avec le style créé précedemment.

## Edition de couches collaboratives


