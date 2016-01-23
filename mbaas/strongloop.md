# StrongLoop
```
export HOST=0.0.0.0
PORT=4000 slc arc
```
## Attacher un modèle à une source de données

## Créer les tables pour les modèles du système
1. Attacher le modèle User à une source de données
2. Créer le fichier server/create-lb-tables.js (Si la base de données contient des tables utiliser autoupdate à la place de automigrate)

```
var server = require('./server');
var ds = server.dataSources.db;
var lbTables = ['User', 'AccessToken', 'ACL', 'RoleMapping', 'Role'];
ds.automigrate(lbTables, function(er) {
  if (er) throw er;
  console.log('Looback tables [' + lbTables + '] created in ', ds.adapter.name);
  ds.disconnect();
});
```

3. Lancer le script

```
$ cd server
$ node create-lb-tables.js
```

## Générer le module client Angularjs

```
$ lb-ng server/server.js client/js/services/lb-services.js
```

## Lancer Arc
```
$ slc arc
```
## Lancer l'application
```
$ node .
```