# TechJam DevOps (Dagger)

Par [Michée Lengronne](https://github.com/micheelengronne)

Ne pas confondre avec [Google Dagger](https://github.com/google/dagger).

## Install

Via un script qui télécharge un asset de release Github et check sa signature.

Le script peut être immutable avec une env `DAGGER_VERSION`.

Dagger nécessite Docker.

## Usage

Dans la VM créée par Vagrant:

```
sudo su
cd /usr/local/src/dagger/pkg/universe.dagger.io/examples
```

Exemple todoapp :

```
cd todoapp
dagger do build
```

Exemple changelog.com (erreur `FTL` pour le moment) :

```
cd changelog.com
dagger do app
```

Exemple helloworld :
```
cd helloworld
dagger do hello
```

### Avantages

Réponse potentielle au problème de vendor-lockin des CI/CD. Actuellement, je fais ça avec des docker-compose et des scripts au sein de ces compose.

Outil potentiel pour la méthodologie [3musketeers](https://3musketeers.io/).
Remplace un makefile avec des notions de dependances et une syntaxe plus lisible.

Intégration avec les outils d'IaC APIfiés (Terraform...).

Le langage CUE permet d'ajouter plus de complexité que ne le peuvent YAML ou JSON nativement.
Ça évite d'imbriquer les DSL et les langages de template entre eux (comme YAML et Jinja par exemple).

Intégration d'un catalogue d'actions pour augmenter le pipeline.

### Inconvénients

Perte potentielle d'accès aux particularités de chaque CI et d'observabilité (tout un pipeline Dagger peut s'exécuter dans un seul job CI).

Écosystème intégré dans Docker. Pas de support Podman ou Vagrant. Je vais devoir continuer à faire des scripts shell et des tasks VSCodium pour ça.

La télémétrie est active par défaut (ah, le RGPD s'envole encore vers une autre galaxie...) mais peut être désactivée avec `DO_NOT_TRACK=1`.
