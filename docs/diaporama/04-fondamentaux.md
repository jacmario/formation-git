<!-- .slide: data-background-image="images/logo-git.png" data-background-size="600px" class="chapter" -->
## 4
### Fondamentaux


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Obtenir un dépôt Git

Transformer un dossier en dépôt Git
 - `git init`
 - Le répertoire `.git/` est créé dans le dossier
 - Il ne contient aucun commit
 - Les fichiers déjà présents sont considérés comme non suivis par Git (_untracked_) 
 
Clôner un dépôt Git distant
 - `git clone <url>`
 - Le dépôt complet est copié à partir de l’url dans un dossier `.git/` local
  - `git clone ssh://git@git.stable.innovation.insee.eu:22222/wehdrc/formation-git.git`
  - &rarr; `formation-git/.git/`
 - La dernière version de la branche `master` est extraite
 - Le dépôt local reste connecté au dépôt distant
  - `cat .git/config` :

```bash
[remote "origin"]
	url = ssh://git@git.stable.innovation.insee.eu:22222/wehdrc/formation-git.git
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Le cycle de vie du statut des fichiers
<div class="center">
	<img src="images/lifecycle.png" /> 
</div>


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Connaitre l’état des fichiers du dépôt : `git status`
```bash
> git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
	(use "git push" to publish your local commits)
Changes to be committed:
	(use "git reset HEAD <file>..." to unstage)

		modified:		docs/diaporama/slides.css
		new file:		docs/images/basic-rebase-1.png
		modified:		docs/index.html

Changes not staged for commit:
	(use "git add <file>..." to update what will be committed)
	(use "git checkout -- <file>..." to discard changes in working directory)

		modified:		docs/diaporama/03-configuration.md
		modified:		docs/diaporama/slides.css
		modified:		docs/images/egit-add.png

Untracked files:
	(use "git add <file>..." to include in what will be committed)

		docs/images/basic-rebase-2.png
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Version courte : `git status --short`
 
 - colonne de gauche = copie de travail
 - colonne de droite = index

```bash
> git status -s
 M	docs/diaporama/03-configuration.md
MM	docs/diaporama/slides.css
A	 docs/images/basic-rebase-1.png
M	 docs/index.html
??	docs/images/basic-rebase-2.png
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Indexer des fichiers : `git add`
Indexer un fichier en particulier :
```bash
git add src/main/java/fr/insee/bar/controller/AccueilController.java
```

Indexer plusieurs fichiers à la fois :
```bash
# Tous les fichiers du répertoire src/ et de ses sous-répertoires
git add src

# Tous les fichiers se terminant par « .java »
git add "*.java"
```

Indexer tous les fichiers modifiés du répertoire courant :
```bash
git add .
```

Désindexer : `git reset`
```bash
git reset src/main/java/fr/insee/bar/controller/AccueilController.java # un seul fichier
git reset src # tous les fichiers d'un répertoire
git reset "*.java" # tous les fichiers se terminant par « .java »
git reset . # tous les fichiers du répertoire courant
```


%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Indexer avec EGit dans Eclipse

Résultat de la commande `git status -s` :
```bash
 M	docs/diaporama/03-configuration.md
MM	docs/diaporama/slides.css
A	 docs/images/basic-rebase-1.png
M	 docs/index.html
??	docs/images/basic-rebase-2.png
```

L’interface graphique est ici clairement un atout :
<div class="center">
	<img src="images/egit-add.png" /> 
</div>



%%%


<!-- .slide: class="slide" data-background-image="images/logo-git.png" data-background-size="600px" -->
### Valider des fichiers : `git commit`
Enregistrer le contenu de l'index dans l'historique local :
```bash
git commit
```
 - l'éditeur de texte configuré s'ouvre
 - il faut saisir un message de _commit_
  - message vide &rarr;  _commit_ annulé
  - les lignes qui commencent par `#` ne comptent pas
 - rappel pour quitter `vi` :
  - sauvegarder et quitter : `Esc` puis `:wq` ou `ZZ` 
  - quitter sans sauvegarder : `Esc` puis `:q!`

Saisir le message tout de suite : `git commit --message` :
```bash
git commit -m "Message de validation explicite"
```

Valider tous les fichiers à l'état modifié : `git commit --all`
 - sans passer par l'index (`git add`)
 - ne comprend pas les fichiers non suivis (_untracked_)

```bash
git commit -am "Message de validation explicite"
```