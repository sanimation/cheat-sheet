# GIT
Cf. la documentation complète [içi](https://git-scm.com)
## Création
Cloner un dépôt existant

```$ git clone ssh://user@domain.com/repo.git```

Créer un dépôt local

```$ git init```
## Changements en local
Voir les changements dans votre environnement de travail

```$ git status```

Voir les changements des fichiers sous controle de version

```$ git diff```

Ajouter tous les changements courants au prochain commit

```$ git add .```

Ajouter les changements réalisés dans le fichier <file> au prochain commit

```$ git add -p <file>```

Commiter tous les changements

```$ git commit -a```

Commiter les changements précédemment effectués

```$ git commit```

Modifier le dernier commit (ne modifie pas les modifications déjà publiées)

```$ git commit --amend```

## Configurer un utilisateur

Quand on utilise git, pour pouvoir faire un commit la première fois, il faut s'identifier.

### En ligne de commande

```$ git config —global user.email “you@example.com"```

```$ git config —global user.name “Votre nom"```

### Via un fichier de config
Dans le fichier .gitconfig:
```
[user]
  name=Votre nom
  email=you@example.com```
  
## Mise à jour et publication
Lister tous les dépôts distants

```$ git remote -v```

Visualiser plus d'informations à propos d'un dépôt distant particulier  

```$ git remote show <remote>```

Ajouter un dépôt distant

```$ git remote add <shortname> <url>```

Récupérer tous les changements du dépôt distant sans l'intégrer à HEAD

```$ git fetch <remote>```

Récupérer tous les changements du dépôt distant et merger/integrer à HEAD

```$ git pull <remote> <branch>```

Publier vos modifications sur le dépôt distant

```$ git push <remote> <branch>```

Supprimer une branche du dépôt distant

```$ git branch -dr <remote/branch>```

Publier les tags sur le dépôt distant

```$ git push <remote> --tags```