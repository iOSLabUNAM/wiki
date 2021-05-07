---
title: Git Cheatsheet
category: appendix
layout: post
---

## Configuracion inicial

Configurar email

    $ git config --global author.email <my emails>

Configurar nombre

    $ git config --global author.name "<my name>"

Configurar mergetool

    $ git config --global merge.tool opendiff

## Inicializar repositorio

Inicializar control de versiones en el directorio actual

    $ git init .

Clonar repositorio existente

    $ git clone <remote url .git>


## Adds & Commits

Agregar archivos al control de versiones

    $ git add <file>

Agregar cambios selectivamente al control de versiones

    $ git add <file> -p

Realizar un commit

    $ git commit -m "here goes a message"

## Repositorios remotos

Agregar repositorio remoto

    $ git remote add <remote_name> <git repo url>

Descargar todas las ramas

    $ git fetch

Descargar cambios a repositorio remoto

    $ git pull <remote_name> <branch>

Subir cambios a repositorio remoto

    $ git push <remote_name> <branch>

## Informacion

Status actual de cambios

    $ git status

Diferencias en cambios

    $ git diff

Historial de cambios

    $ git log

Historial de cambios en una sola linea

    $ git log --oneline

## Branches

Crear branch

    $ git branch <my-branch-name>

Renombrar branch actual

    $ git branch -m <my-new-branch-name>

Borrar rama local

    $ git branch -D <branch name>

Borrar rama remota

    $ git push <remote> :<branch name>

Moverse a rama

    $ git checkout <branch-name>

Moverse a rama y crearla

    $ git checkout -b <branch-name>

Poner cambios en la rama temporal **stash**

    $ git stash

Extraer de pila de la rama temporal

    $ git stash pop

## Merge & Rebase

Combinar branch a la rama actual

    $ git merge <branch name>

Rebasar cambios en local

    $ git rebase <branch name>

Poner los cambios de la rama adelante de una rama remota

    $ git pull --rebase <remote> <branch name>

## Comandos Avanzados

Squash commits con autorebase

    $ git rebase -i <commit hash>

Cherry Pick

    $ git cherry-pick <commit hash>
