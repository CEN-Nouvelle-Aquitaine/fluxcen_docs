# Utiliser FluxCEN

FluxCEN étant développé pour être utilisé au sein du SI d'un organisme, il n'est pas publié dans le dépôt officiel des plugins QGIS.
Dans un objectif de déploiement automatique, il doit donc donc être hébérgé dans un dépôt privé.

## 1. Forker le projet

Forkez le [dépôt GitHub de FluxCEN](https://github.com/CEN-Nouvelle-Aquitaine/fluxcen) dans votre organisation directement depuis GitHub.

Cloner ce nouveau dépôt localement.

## 2. Configurer le nouveau dépôt

Le dépôt source étant le FluxCEN utilisé en production par le CEN Nouvelle-Aquitaint, il convient de procéder à quelques ajustements avant de commencer.


### 2.1 Créer et éditer les fichiers de configuration

Deux fichiers de configurations sont nécessaires pour le bon fonctionnement du plugin. Ils sont ajoutés au fichier `.gitignore` afin de ne pas être véhiculés publiquement sur le git. 

Il faut donc les créer, en utilisant les deux fichiers exemples situés dans `config/yaml`.

</br>

Le fichier `links.yaml` est la clé de voûte du plugin. Il assure le lien entre le plugin et le git et évite ainsi de devoir publier une nouvelle version du plugin à chaque fois que le fichier flux.csv est modifié par exemple.

```yml
github_urls:
  flux_csv: "link_to_the_csv_file (your_flux.csv)"
  styles_couches: "link_to_the_layer_styles_file (your styles_couches folder)"
  info_changelog: "link_to_the_changelog_html (if needed)"
depot_plugins_url:
  last_version: "link_to_the_plugin_version (.txt)"
```
Les liens sont à copier depuis l'application web GitHub en prenant soin de sélectionner l'option `Raw` afin d'avoir accès au fichier brut.

</br>

Le fichier `config_db.yaml` est optionnel et doit être configuré si on veut utiliser l'édition collaborative de couches PostGIS. Il accueille ainsi la configuration de l'accès au cluster de base de données.

```yml
database:
  - type: PostGIS
    host: your_database_ip
    port: your_database_port (5432 by default)
```

### 2.1 Modifier le fichier flux.csv

Afin d'utiliser ses propores flux, il faut maintenant modifier le fichier `flux.csv`.
Le plus simple est de supprimer le fichier existant puis partir du fichier `flux_example.csv` qui rassemble un certain nombre de ressources nationales (IGN, INPN, etc.) en le renommant.

Vous pouvez également supprimer tous les fichiers dans le dossier `styles_couches` afin de partir d'une base propre.


## Publier sur son propre dépôt de plugins QGIS

Une fois la configuration effectuée et le fichier flux.csv personnalisé, vous êtes prêt à publier le plugin après un commit des modifications.

