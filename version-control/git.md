# GIT
## Création
Cloner un repository existant
```
$ git clone ssh://user@domain.com/repo.git
```
Créer un repository local
```
$ git init
```
## Changements en local
Changements dans votre environnement de travail
```
$ git status
```
Changements des fichiers sous controle de version
```
$ git diff
```
Ajouter tous les changements courants au prochain commit
```
$ git add .
```
Ajouter les changements réalisés dans le fichier <file> au prochain commit
```
$ git add -p <file>
```
Commiter tous les changements
```
$ git commit -a
```
Commiter previously staged changes
```
$ git commit
```
Modifier le dernier commit (ne modifie pas les modifications déjà publiées)
```
$ git commit --amend
```
## Configurer un utilisateur
Quand on utilise git, pour pouvoir faire un commit la première fois, il faut s'identifier.
### En ligne de commande
```
git config —global user.email “you@example.com"
git config —global user.name “Votre nom"
```
### Via un fichier de config
Créer un fichier .gitconfig:
```
[user]
  name=Votre nom
  email=you@example.com
```
