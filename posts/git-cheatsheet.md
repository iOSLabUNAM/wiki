---
title: Git Cheat Sheet
category: annex
---

# Git Cheat Sheet

Inicializar control de versiones en el directorio actual

    $ git init .

Agregar archivos al control de versiones

    $ git add <file>

Agregar cambios selectivamente al control de versiones

    $ git add <file> -p

Realizar un commit

    $ git commit -m "here goes a message"

Agregar repositorio remoto

    $ git remote add <remote_name> <git repo url>

Descargar todas las ramas

    $ git fetch

Descargar cambios a repositio remoto

    $ git pull <remote_name> <branch>

Subir cambios a repositio remoto

    $ git push <remote_name> <branch>

Status actual de cambios

    $ git status

Poner cambios en la rama fantasma **stash**

    $ git stash

Extraer de pila de la rama fantasma

    $ git stash pop

Rebasar cambios en local

    $ git rebase <branch name>

Poner los cambios de la rama adelante de una rama remota

    $ git pull --rebase <remote> <branch name>

Combinar branch a la rama actual

    $ git merge <branch name>

Borrar rama local

    $ git branch -D <branch name>

Borrar rama remota

    $ git push <remote> :<branch name>

Historial de cambios

    $ git log

Historial de cambios en una sola linea

    $ git log --oneline

Auto rebase

    $ git rebase -i <commit hash>


Cherry Pick

    $ git cherry-pick <commit hash>
