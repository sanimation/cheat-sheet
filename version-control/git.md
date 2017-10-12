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

## Undo a commit and redo

`$ git commit -m "Something terribly misguided" `             (1)
`$ git reset HEAD~  `                                         (2)
<< edit files as necessary >>                               (3)
`$ git add ... `                                              (4)
`$ git commit -c ORIG_HEAD`                                   (5)

1. This is what you want to undo
2. This leaves your working tree (the state of your files on disk) unchanged but undoes the commit and leaves the changes you committed unstaged (so they'll appear as "Changes not staged for commit" in git status, and you'll need to add them again before committing). If you only want to add more changes to the previous commit, or change the commit message1, you could use git reset --soft HEAD~ instead, which is like git reset HEAD~ but leaves your existing changes staged.
3. Make corrections to working tree files.
4. git add anything that you want to include in your new commit.
5. Commit the changes, reusing the old commit message. reset copied the old head to .git/ORIG_HEAD; commit with -c ORIG_HEAD will open an editor, which initially contains the log message from the old commit and allows you to edit it. If you do not need to edit the message, you could use the -C option.