---
title: Flujos de trabajo con git
category: design patterns
layout: post
---

![hero](https://wac-cdn.atlassian.com/dam/jcr:25d06843-2468-4e00-8ae7-11d4164f8995/hero.svg?cdnVersion=hp)
La diversidad de metodologias a implementar en los flujos de trabajo pueden difícultar la implementacion GIT en un proyecto colaborativo.

La finalidad de esta wiki es mostrar a grandes rasgos los diferentes flujos de trabajo que pueden ser implementados. Los cuales están diseñados para ser directivas mas que reglas concretas, de esta forma podras mezclar y combinar aspectos de flujos de trabajo diferentes para satisfacer tus necesidades individuales.

## Centralizado
![centralized](https://wac-cdn.atlassian.com/dam/jcr:c27e646e-0b66-49bd-9f85-ee9205e295d6/01.svg?cdnVersion=hp)

Al igual que Subversion, el flujo de trabajo centralizado utiliza un repositorio central para servir como punto de entrada único para todos los cambios en el proyecto. En lugar de *trunk*, la rama de desarrollo predeterminada se denomina *master* y todos los cambios se asignan a esta rama. Este flujo de trabajo no requiere ninguna otra rama además del master.

Los desarrolladores comienzan clonando el repositorio central. En sus propias copias locales del proyecto, editan archivos y realizan cambios como lo harían con SVN; sin embargo, estos nuevos *commits* se almacenan localmente, están completamente aislados del repositorio central. Esto permite a los desarrolladores diferir la sincronización en sentido ascendente hasta que estén en un punto de interrupción conveniente.

Para publicar cambios en el proyecto oficial, los desarrolladores suben *(push)* su rama master local al repositorio central. Éste es el equivalente de svn commit, excepto que agrega todos los commits locales que aún no están en la rama principal central.
![cental-example](https://wac-cdn.atlassian.com/dam/jcr:24d40389-e44e-4c28-b01b-be389d52506d/02.svg?cdnVersion=hp)

## Feature-Branch
![feature-branch](https://wac-cdn.atlassian.com/dam/jcr:f78ecc23-1371-4ce9-b2c0-b7a9fe706b21/01.svg?cdnVersion=hp)
El flujo de trabajo Feature-Branch aún utiliza un repositorio central y el maestro todavía representa el historial oficial del proyecto. Pero, en lugar de commit directamente en su rama `master` local, los desarrolladores crean una nueva `branch` cada vez que comienzan a trabajar en un nuevo feature. Las ramas deben tener nombres descriptivos, como animated-menu-items o issue-1061. La idea es dar un propósito claro y altamente enfocado a cada rama.

Git no hace ninguna distinción técnica entre la rama `master` y las ramas de `feature`, por lo que los desarrolladores pueden realizar cambios en una rama como lo hicieron en el flujo de trabajo centralizado.

Además, las ramas de features pueden (y deben) ser subidas al repositorio central. Esto hace posible compartir una función con otros desarrolladores sin tocar ningún código oficial. Dado que master es la única rama "especial", el almacenamiento de varias ramas de entidades en el repositorio central no plantea ningún problema. Por supuesto, esta es también una manera conveniente de respaldar los commits locales de todos.

### Pull Requests
Aparte de aislar el desarrollo de features, las ramas permiten discutir los cambios a través de **Pull Requests** (solicitudes de cambios). Una vez que alguien completa un feature, no hace `merge` a `master` inmediatamente. En su lugar, sube la rama de feature al repositorio central y crea un Pull Request solicitando el `merge` de sus cambios a la rama principal. Esto da a otros desarrolladores la oportunidad de revisar los cambios antes de que se conviertan en parte de la base de código principal.

La revisión de código es un beneficio importante de las solicitudes de extracción, pero en realidad están diseñadas para ser una forma genérica de hablar de código. Puede pensar en los Pull Request como una discusión dedicada a una rama en particular. Esto significa que también pueden utilizarse mucho antes en el proceso de desarrollo. Por ejemplo, si un desarrollador necesita ayuda con un feature en particular, todo lo que tiene que hacer es crear el Pull Request. Las partes interesadas serán notificadas automáticamente, y podrán ver la pregunta justo al lado de los `commits` pertinentes.

Una vez que se acepta un Pull Request, el acto real de publicar un feature es prácticamente el mismo que en el flujo de trabajo centralizado. Primero, se necesita cerciorarse de que su `master` local esté sincronizado con el `master` del repositorio. Para posteriormente realizar el `merge` de la rama a `master`. En Github este proceso esta automatizado en el boton de *merge*, si hay algun conflicto con master Github deshabilitara dicho boton.

Para ver a mas detalle puedes revisar la [introduccion de github-flow](https://guides.github.com/introduction/flow/)

**Nota**: Esta metodologia se adapta a la metodologia agil de kanban y practicas **XP** (Extreme Programing)

## Gitflow
![gitflow](https://wac-cdn.atlassian.com/dam/jcr:e3bd4199-27ac-4bac-a5d2-3ff0fdb112d3/01.svg?cdnVersion=hp)
El [flujo de trabajo de Gitflow](http://nvie.com/posts/a-successful-git-branching-model/) se deriva de Vincent Driessen en [nvie](http://nvie.com/). Define un modelo de ramas estricto diseñado alrededor de versiones de proyecto. Aunque es un poco más complicado que el flujo de trabajo **feature-branch**, proporciona un marco robusto para administrar proyectos más grandes.

Este flujo de trabajo no añade ningún nuevo concepto o comando más allá de lo requerido para el flujo de trabajo de **feature-branch**. En cambio, asigna roles muy específicos a diferentes ramas y define cómo y cuándo deben interactuar. Además de las ramas de features, utiliza ramas individuales para preparar, mantener y guardar las versiones. También aprovecha todos los beneficios del flujo de trabajo **feature-branch**: pull-requests, experimentos aislados y colaboración más eficiente.

La principal diferencia con el flujo de trabajo **feature-branch**, es que se añade un paso intermedio entre `master` y las ramas de `feature` si bien puede ser una rama denominada `development` o `release-#<numero de release>` que funge como paso previo a publicar a `master`.

**Nota**: Esta metodologia se adapta a la metodologia agil de scrum ya que se pueden establecer ramas de relase por sprint.

## Forking
![forking](https://wac-cdn.atlassian.com/dam/jcr:5c0941ff-a8b5-435b-a092-2167705f1e97/01.svg?cdnVersion=hp)

La principal ventaja del flujo de trabajo de **Forking** es que las contribuciones se pueden integrar sin la necesidad de que todo el mundo suba a un único repositorio central. Los desarrolladores suben a sus propios repositorios del lado del servidor, y sólo el responsable del proyecto puede pasar al repositorio oficial. Esto permite al mantenedor aceptar commits de cualquier desarrollador sin darles acceso de escritura al codigo base oficial.

El resultado es un flujo de trabajo distribuido que proporciona una forma flexible para que los grandes equipos orgánicos (incluidos los terceros no confiables) colaboren de forma segura. Esto también lo convierte en un flujo de trabajo **ideal para proyectos de código abierto**.

Al igual que en los otros flujos de trabajo de Git, el flujo de trabajo de Forking comienza con un repositorio público oficial almacenado en un servidor. Pero cuando un nuevo desarrollador quiere comenzar a trabajar en el proyecto, no clonan directamente el repositorio oficial.

En su lugar, se realiza un **Fork** en el repositorio oficial para crear una copia del mismo en el servidor. Esta nueva copia sirve como su repositorio público personal; no se permite a otros desarrolladores subir hacia él, pero pueden extraer cambios de él. Después de haber realizado el Fork el desarrollador clona en ambiente local de git para obtener una copia de él.

Cuando están listos para publicar un commit local, suben el commit a su propio repositorio público, no el oficial. A continuación, crean un pull-request a el repositorio principal, lo que permite al responsable del proyecto saber que una actualización está lista para ser integrada. El pull request también sirve como para mantener una conversacion conveniente si hay problemas con el código aportado.

Para integrar la característica en la base de código oficial, el mantenedor acepta el pull request del contribuyente en su repositorio, comprueba que no rompa el proyecto, hace merge a `master` de origen. La contribución es ahora parte del proyecto, y otros desarrolladores deben hacer `pull` del repositorio oficial para sincronizar sus repositorios locales.

---
[Fuente Original](https://www.atlassian.com/git/tutorials/comparing-workflows)
