# StrongLoop
```
export HOST=0.0.0.0
PORT=4000 slc arc
```
# Attacher un modèle à une source de données

# Créer les tables pour les modèles du système
1. Attacher le modèle User à une source de données
2. Créer le fichier server/create-lb-tables.js
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


