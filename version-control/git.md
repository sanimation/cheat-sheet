# GIT
## Création
Cloner un dépôt existant

```$ git clone ssh://user@domain.com/repo.git```

Créer un dépôt local

```$ git init```
## Changements en local
Changements dans votre environnement de travail

```$ git status```

Changements des fichiers sous controle de version

```$ git diff```

Ajouter tous les changements courants au prochain commit

```$ git add .```

Ajouter les changements réalisés dans le fichier <file> au prochain commit
```
$ git add -p <file>
```
Commiter tous les changements
```
$ git commit -a
```
Commiter les changements précédemment effectués
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
Dans le fichier .gitconfig:
```
[user]
  name=Votre nom
  email=you@example.com
```
## Mise à jour et publication
Lister tous les dépôts distants
```
$ git remote -v
```
Show information about a remote
```
$ git remote show <remote>
```
Add new remote repository, named <remote>
```
$ git remote add <shortname> <url>
```
Download all changes from <remote>,
but don‘t integrate into HEAD
```
$ git fetch <remote>
```
Download changes and directly
merge/integrate into HEAD
```
$ git pull <remote> <branch>
```
Publish local changes on a remote
```
$ git push <remote> <branch>
```
Delete a branch on the remote
```
$ git branch -dr <remote/branch>
```
Publish your tag s
```
$ git push --tags
```