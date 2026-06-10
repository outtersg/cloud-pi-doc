# Gestion des déploiements

Depuis la console il est possible de créer des déploiements applicatifs pour son projet.

Un déploiement permet d'associer un environnement à un ou plusieurs dépôts de code d'infrastructure.

La console génère ensuite la configuration ArgoCD correspondante afin de déployer les ressources dans le namespace de l'environnement cible.

## Créer un déploiement

Depuis la console, aller dans l'onglet *Ressources* d'un projet.

![Liste des déploiements](/img/guide/deployment/liste-deploiements.png)

Dans la partie **Déploiements**, cliquer sur le bouton **+ Ajouter un nouveau déploiement** puis compléter :

- Un nom de déploiement, par exemple `api` ou `front`
- L'environnement cible du déploiement
- Le ou les dépôts à inclure dans ce déploiement

![Création d'un déploiement](/img/guide/deployment/creation-deploiement.png)

> Un déploiement est toujours rattaché à un seul environnement.

## Configurer les dépôts du déploiement

Pour chaque dépôt inclus dans un déploiement, il est possible de configurer :

- **Dépôt** : le dépôt à déployer.
- **Nom de la révision à déployer** : branche, tag ou commit à utiliser. Si le champ est vide, la cible sera `HEAD`.
- **Chemin du répertoire à déployer** : chemin vers les manifests, kustomize ou chart Helm. Si le champ est vide, la racine du dépôt sera utilisée.
- **Fichiers values (Helm)** : un fichier par ligne, chemin relatif par rapport au répertoire à déployer.

Exemple :

```text
values/common.yaml
values-other/custom.yaml
```

## Multi branches et target revision

Un même dépôt peut être déployé sur plusieurs environnements avec une révision différente.

Par exemple :

- `integration` peut déployer la branche `develop`
- `staging` peut déployer la branche `release`
- `production` peut déployer un tag ou un commit précis

Cette configuration se fait depuis le déploiement, dans le champ **Nom de la révision à déployer** de chaque dépôt.

## Multi dépôts

Un déploiement peut contenir plusieurs dépôts.

Ce mode permet par exemple de déployer, sur un même environnement :

- un dépôt contenant les manifests communs
- un dépôt contenant le chart Helm applicatif
- un dépôt contenant une configuration spécifique

Chaque dépôt garde sa propre configuration de révision, de chemin et de fichiers values.

## Synchronisation ArgoCD

La console reste la source de vérité pour la configuration des déploiements.

Les modifications doivent être faites depuis la console et non directement depuis l'application ArgoCD.

Après création ou modification d'un déploiement, la console met à jour la configuration ArgoCD du projet. Le déploiement est ensuite synchronisé par ArgoCD.

Pour plus de détails sur la visualisation et la synchronisation dans ArgoCD, voir [Déploiement de votre application](/guide/deployment-with-argo).

> Si aucun déploiement n'est configuré, la console conserve le fonctionnement basé sur les dépôts d'infrastructure déclarés dans le projet.
