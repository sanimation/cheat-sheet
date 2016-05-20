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

## Générer les services avec le SDK loopback Angularjs

```
$ lb-ng ./server/server.js ./client/js/services.js
```

## Lancer Arc
```
$ slc arc
```
## Lancer l'application
```
$ node .
```

```
$ DEBUG=loopback:security:* node .
```

## L'explorer
### Filtrer les résultats du find
```
{"filter": {"order": "id DESC", "limit": "10"}}
```
```
{"where": {"subscriptions": ["2","3"]}}
```
```
{"where": {"serviceId" : "2"}, "fields": {"subscriberId": "true"}}
```

```
{"include": "service"}
```

### Envoyer un Push
Dans le champ devicequery
```
{"appId": "fr.efficiencesoftware.newsfeed", "subscriptions": [2,3]}
```

subscriptions: {inq: subscriptions}
 
Dans le champ notification:
```
{
"alert": "test"
}
```

### Login

```{"email":"foo@bar.com","password":"foobar"}```