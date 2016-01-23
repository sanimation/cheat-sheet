# OpenShift

Cf. [doc](https://strongloop.com/strongblog/node-js-rest-api-openshift-redhat/)

## Créer un compte Open Shift

```$ sudo gem install rhc```

## Créer l'application

```$ rhc app create MyApi https://raw.github.com/strongloop/openshift-cartridge-strongloop/master/metadata/manifest.yml```

## Déployer
Voir les info de connexion:

```$ rhc app show myapi```

Mettre à jour l'appli:

```
$ git remote add openshift ssh://5400b85c5004467ec9000337@myapi-strongdemo.rhcloud.com/~/git/myapi.git/
$ git push --force openshift master
```
