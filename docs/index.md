# =="Un plugin QGIS pour les rassembler tous"==

Le plugin QGIS FluxCEN permet d'accéder rapidement à un large éventail de flux WFS/WMS organisés par catégories et interrogeables sous forme de mots-clés.

Il rend également possible l'édition de "couches SIG collaboratives" grâce à la prise en charge de l'édition de tables du SGBD PostgreSQL/PostGIS.

Il évite ainsi d'avoir à gérer dans QGIS une multitude de connexions et simplifie grandement l'accès aux données dans un système d'information.

Grâce au lien direct avec le dépôt GitHub, l'ajout et la modification des ressources ne nécessite pas de publier à chaque fois une nouvelle version du plugin.



## Génèse




## Principe de fonctionnement

* `Centralisation et gestion des flux simplifiée dans un fichier .csv au sein de catégories`
* `Recherche rapide des ressources par autocomplétion`
* `Lien direct vers l'URL de la fiche de métadonnées pour chaque flux`
* `Mise à jour des flux directement depuis le git`
* `Prise en charge des flux GeoServer et MapServer`

### Fonctionnalités additionnelles

* `Gestion des styles au format .qml à l'ouverture dans QGIS pour les données WFS`
* `Fonction d'édition : accès à des tables PostgreSQL/PostGIS pour l'édition collaborative avec gestion du formulaire de saisie`


## Auteurs

* [Romain MONTILLET](https://github.com/wanderzen91) est le développeur principal du plugin
* [Thomas GACHET](https://github.com/tomgachet) est à l'origine du projet et apporte quelques contributions et idées 