#Les fonctionnalités en détail

## :material-file-delimited-outline: Le fichier *flux.csv*

Situé à la racine du projet, le fichier ***`flux.csv`*** est le coeur de l'application. C'est lui qui centralise toutes les ressources et permet l'affichage de ces dernières dans le plugin.

Voici sa description et l'utilisation des champs selon le type de service consulté (les champs en gras sont visibles dans le plugin) :

| Nom du champ       | Description                          | WMS | WFS | PostGIS |
| :----------------  | :----------------------------------- |     |     |         |
| **`service`**        | Type de service utilisé (WFS, WMS, PostGIS) | :material-check: | :material-check: | :material-check:|
| `categorie`        | Categorie de rattachement de la ressource pour affichage et recherche dans le plugin  | :material-check: | :material-check: | :material-check:|
| **`Nom_couche_plugin`**| Nom de la ressource qui s'affichera dans le plugin | :material-check: | :material-check: | :material-check:|
| `nom_technique`    | Nom de la ressource utilisé sur le serveur source (nom de la table pour le service PostGIS) | :material-check: | :material-check: | :material-check:|
| `url`              | URL du serveur d'accès à la ressource | :material-check: | :material-check: | :material-close: |
| **`source`**           | Source de la donnée (producteur) | :material-check: | :material-check: | :material-check: |
| `style`            | Nom du fichier de style *.qml* situé dans le dossier *styles_couches* pour affichage à l'ouverture dans QGIS (voir ci-dessous) | :material-close: | :material-check: | :material-close: |
| **`metadonnees`**      | URL de la fiche de métadonnées liée à la resource | :material-check: | :material-check: | :material-check:|
| `nom_bdd`          | Nom de la base de données | :material-close: | :material-close: | :material-check:|
| `nom_schema`       | Nom du schéma | :material-close: | :material-close: | :material-check:|

</br>

## :material-brush: **Styles des ressources dans QGIS**

### :material-vector-polyline-edit: Paramétrer les styles

Les différentes ressources peuvent être chargées dans QGIS avec un style par défaut selon le service consulté.

* **WFS**

Le style n'étant pas géré par le serveur cartographique source, il faut créer un fichier de style dédié :

1. Ouvrir le flux dans QGIS
2. Paramétrer le style et l'enregistrer au format *`.qml`* (voir la section *Attacher des formulaire (UI)* en fin de page pour embarquer un formulaire)
3. Déposer ce fichier *.qml* nouvellement créé dans le dossier *`styles_couches`* du git
4. Indiquer le nom du fichier dans la colonne *style* du fichier *flux.csv* pour la ressource concernée
---

* **WMS**

Le style n'est pas géré dans FluxCEN mais directement par le serveur cartographique source au format *`.sld`*.

---

* **PostGIS**

Le style par défaut peut être enregistré directement dans la base de données source :

1. Ouvrir la table dans QGIS
2. Paramétrer le style et l'enregistrer dans la base de données source *(Propriétés de la couche / Style / Enregistrer le style / in datasource database)* en cochant la case *Utiliser comme style par défaut pour cette couche* (voir la section *Attacher des formulaire (UI)* ci-dessous pour embarquer un formulaire)

!!! tip "Bon à savoir"

    :fontawesome-solid-database: 
    Une table *layer_styles* est créée automatiquement dans le schéma *public* de la base de données source. Le style est généré en *qml* dans le champ *styleqml*.

### :material-form-select: Attacher un formulaire (UI)

Il peut être intéressant d'embarquer dans le style un formulaire *`.ui`* pour une meilleure consultation et/ou édition des données dans QGIS.

1. Créer et tester le formulaire via *Qt Designer*
2. Déposer le *.ui* dans le dossier *`styles_couches`* du git
3. Récupérer l'URL publique d'accès depuis le git vers ce fichier nouvellement déposé (accès brut via l'option `Raw`)
4. Coller cette URL dans le champ *Éditer interface* lors du paramétrage du style dans QGIS *(Propriétés de la couche / Formulaire d'attributs)* puis selectionner *À partir du fichier .ui fourni*

L'accès au formulaire *.ui* est ainsi directement intégré au *.qml* (fichier en dur pour WFS ou champ de base de données pour PostGIS).

!!! example "Pratique"

    Le formulaire *.ui* peut être désormais mis à jour directement depuis le git!
</br>

## :material-lock-check-outline: Accès aux flux protégés

Si l'accès à la majorité des ressources reste public, certaines peuvent être protégées par un couple *identifiant/mot de passe* (données métier confidentielles par exemple).

L'accès à une table PostGIS nécessitera toujours quand à elle une connexion de ce type.

Cette authentification n'est pas gérée depuis FluxCEN mais doit être **configurée depuis les serveurs** véhiculant les ressources :

* depuis le serveur cartographique (type GeoServer) pour les flux WMS/WFS
* depuis le serveur de bases de données pour les tables PostGIS.

Pour accéder au ressources protégées, il faut créer en amont une authentification de type *`Basic authentication`* dans QGIS *(Préférences/Options/Authentification)*. Cela évite de devoir saisir à chaque fois son identifiant et son mot de passe à l'ouverture d'une ressource protégée.

Si aucune authentification n'est trouvée par QGIS, un message informe de la nécessité d'en paramétrer une.