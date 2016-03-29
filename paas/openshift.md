# OpenShift

Cf. [doc](https://strongloop.com/strongblog/node-js-rest-api-openshift-redhat/)

## Créer un compte Open Shift

Créer un compte puis installer le gem:

```
$ sudo gem install rhc
```

Ajouter le serveur MySql

## Créer l'application
Créer l'application loopback:
```
$ rhc app create <app_name> https://raw.github.com/strongloop/openshift-cartridge-strongloop/master/metadata/manifest.yml
```

## Déployer
Voir les info de connexion:

```
$ rhc app show <app_name>
```

Mettre à jour l'appli:

```
$ git remote add openshift ssh://5400b85c5004467ec9000337@<app_name>-<domain>.rhcloud.com/~/git/<app_name>.git/
$ git push --force openshift master
```

## Créer les tables

Accès à distance:

```
$ rhc ssh <app_name>
```

Se placer sous le répertoire server dans l'appli et lancer le script de création des tables:

```
$ cd app-root/repo/server
$ node create-lb-tables.js
```

## Log

```
$ rhc tail -a myapp
```