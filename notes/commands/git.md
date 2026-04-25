# Git Commands

## Les trois zones de Git

| Zone | Description |
|---|---|
| Working Directory | Ton dossier local. Tous les fichiers visibles dans VSCode. Les modifications existent uniquement ici jusqu'à ce que tu les ajoutes. |
| Staging Area | Zone d'attente pré-commit. Tu choisis exactement quels fichiers tu veux inclure dans ton prochain snapshot. |
| Repository local | L'historique permanent sur ton ordinateur. Chaque commit est gravé ici avec un identifiant unique et ne disparaît jamais. |
| GitHub | La copie distante du repository. Elle existe sur les serveurs de GitHub, pas sur ton ordinateur. |

## Flux complet

```
Working Directory → Staging Area → Repository local → GitHub
     (on code)        (git add)      (git commit)     (git push)
```

## git add
`git add .` est la commande qui fait passer les fichiers du Working Directory vers la Staging Area. Elle rassemble tous les fichiers qui ont été modifiés vers une aire d'attente pré-commit. Si on remplace le `.` par un nom de fichier, seul le fichier nommé y sera placé.

## git commit
`git commit -m "message"` est le passage des fichiers en Staging Area vers un commit — c'est une sauvegarde locale avant le push. `-m ""` permet de donner un titre au commit. Cela permet d'avoir un suivi clair et ordonné de ce qui est fait. Un historique de commits bien décrit raconte le développement du projet — il doit être clair et précis.

## git push
`git push` est l'action finale qui transfère le commit (privé) vers GitHub (public).