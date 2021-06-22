---
title: Versionado y uso de branches 
category: foundations
layout: post
---

# Versionado y uso de branches 

## ¿Para qué?
En desarrollo es necesario tener un lugar centralizado en donde se almacenan los proyectos que se desarrollan disponibles para cualquier developer teniendo un historial de cambios con responsables asignados.

## ¿Qué areas lo necesitan?
- Equipo de desarrollo (FrontEnd, BackEnd, Data Análisis)
- Producción
- Devops

## Repositorios
Es usual que las empresas usen herramientas de versionado como lo son GitHub y GitLab, pero además de usar estas herramientas, es necesario tener buenas practicas en el nombrado de los proyectos, así como del uso de branches. Abajo se expone algunos ejemplos de como usar el nombrado de repositorios:

| Name | Descripción |
| :---: | :---: |
| Versión  | `Números: V1, V2, V4, etc ` >> `Core del negocio: Administración, Finanzas, Cobros` >> `Por años: 2021, 2020, 2019, etc.` >> `O bien una forma creativa usando nombres propios o acronimos: anaconda, boa, zebra, yak` |
| Tipo  | `ms - Microservicio` > `fn - Lambda Function (Azure Function)` > `fw - Framework` > `back - Backend` > `front - Frontend` > `npm - Librería para npm` > `nuget - Librería para nuget` > `int - integración con otra aplicación` > `mig - migraciones de otras aplicaciones` |
| Descripción del proyecto | Descripción breve del nombre del proyecto. En algunos casos puede incluir el módulo al que corresponde. Siempre-va-separado-por-guiones-medios |

De esta manera, un ejemplo para un microservicio que se encarga de crear y manejar notificaciones, que será usado en un ERP, pordría llamarse de la siguiente manera:
> erp-ms-pending-item

## Branches

Dentro del sistema de control de versiones distribuido (DVCS) para llevar el flujo de trabajo y código así como el control de las liberaciones necesitamos llevar un proceso organizado.

Para esto de los repositorios centrales (origin) deberán existir branches con una nomenclatura y rol específicos, facilitando varios aspectos como el trabajo asincrono y paralelo del equipo, visibilidad del estado de desarrollo de los features, etc.

### Branches principales

El repositorio principal siempre tendrá estos 2 los cuáles tienen en común que nunca mueren (como José  José): Master y Develop.

#### Master

Aquí sólo se encuentra código que está **listo para producción** por lo que es la versión estable de todos los proyectos de un producto.

*Quién usa estas ramas:*
- Branches que nacen de master
- Branches que se unen a master
- Enviroments que despliegan usando master

#### Develop

Aquí se encuentra el código que tiene los ultimos cambios para el siguiente release, cuando los cambios que se encuentran en este branch son validados y se encuentran en un estado estable deben de ser unidos a master por medio de un nuevo release.

*Quién usa estas ramas:*
- Branches que nacen de develop
- Branches que se unen a develop
- Enviroments que despliegan usando develop

#### Feature

Estos branches son utlizados para desarrollar los nuevos features de los proyectos. Tienen un ciclo de vida definido el cual acaba hasta que se finaliza el feature en el cual se está trabajando. La forma de nombrar estos branches deberá de respetar el patrón **feature/<feature-name/id>.** Para unir un branch de feature a develop deberá hacerse por medio de un PR.

*Quién usa estas ramas:*
- Branches que nacen de feature/*
- Branches que se unen a feature/*
- Branches de los que nace feature/*
- Branches a los que se une feature/*
- Enviroments que despliegan usando feature/*

#### Release

Estos branches son usandos para preparar una liberación a producción, aquí se pueden resolver **PEQUEÑOS** bugs/features que se detecten **antes de la liberación** así como actualizar la información del proyecto como versión, cambios (changelog) y documentación. **Estas operaciones son realizadas aquí para liberar develop para que allí se unan los nuevos cambios que servirán para el próximo release.**

El momento de crear este branch es cuando está lo suficientemente estable y con los features necesarios para la siguiente liberación, el criterio para colocar el número del release se expondrá más abajo.

La nomenclatura a seguir para este branch es la siguiente **release/x.x.x**

*Quién usa estas ramas:*
- Branches que nacen de release/*
- Branches que se unen a release/*
- Branches de los que nace release/*
- Branches a los que se une release/*
- Enviroments que despliegan usando release/*

#### Fix
Estos branches son utlizados para desarrollar fix pequeños dentro de los proyectos, que pueden surgir del feedback provisto por QA al hacer la revisión de un nuevo feature o bien un fix de una funcionalidad que ya esta en producción que no es bloqueante o bien es una mejora en un flujo, para optimizaciónes o sugerencias del usuario. Tienen un ciclo de vida definido el cual acaba hasta que se finaliza el fix en el cual se está trabajando. La forma de nombrar estos branches deberá de respetar el patrón **fix/<fix-name/id>.** Para unir un branch de fix a develop deberá hacerse por medio de un PR.

*Quién usa estas ramas:*
- Branches que nacen de fix/*
- Branches que se unen a fix/*
- Branches de los que nace fix/*
- Branches a los que se une fix/*
- Enviroments que despliegan usando fix/*

#### Hotfix

Este branch es usado cuando un error se presenta en producción (código que está en master) y necesita resolverse inmediatamente. Se usa para aislar el bug de master y no afectar el trabajo del equipo que esta agregando y desarrollando los features para el siguiente release en develop. Sigue la misma mecánica que los de release así que se tiene que actualizar la información del proyecto (versión del proyecto, changelog, actualización de documentación)

La nomenclatura a seguir para este branch es la siguiente **hotfix/x.x.x**

*Quién usa estas ramas:*
- Branches que nacen de hotfix/*
- Branches que se unen a hotfix/*
- Branches de los que nace hotfix/*
- Branches a los que se une hotfix/*
- Enviroments que despliegan usando hotfix/*

### Versionado

#### ¿Por qué?

Debido a que en una emprese se tienen varios proyectos que tienen muchas dependencias tenemos que tener un control para versionar nuestros productos de forma que con sólo leer la versión podamos identificar el estatus de un proyecto.

Este sistema es un estándar llamado **[Semantic Versioning 2.0.0](https://semver.org/)** usa 3 números los cuáles se usan de esta forma.

> MAJOR.MINOR.PATCH

#### Major

Este es usado para indicar cambios que son incompatibles con versiones anteriores.

Por ejemplo el proyecto A usa como dependencia la versión 1.10.2 de B, si quiere usar la versión 2.0.1 de B, deberá de hacer los cambios pertinentes antes, ya que es seguro que varías cosas cambien lo cuál generaría bugs.

#### Minor

Es usado para indicar que nuevos features fueron agregados y que son compatibles con versiones anteriores.

Por ejemplo el proyecto A usa como dependencia la version 1.10.2 de B, si quiere usar la versión 1.11.0 de B no debería de tener que realizar ningún cambio a menos que quiera implementar los nuevos features de la versión

#### Patch

Es usado para indicar bugs que fueron reparados y que son compatibles con versiones anteriores.

Por ejemplo el proyecto A usa como dependencia la version 1.10.2 de B, si quiere usar la versión 1.10.3 de B no debería de tener que realizar ningún cambio a menos que quiera implementar los nuevos features de la versión

![versioning-standar](/wiki/assets/img/versioning.png)

#### Reglas

1. Un número de versipon normal deberá tomar la siguiente estructura:  X.Y.Z donde  X, Y, y  Z son números enteros positivos, y no deberpa contener ceros a la izquierda. X corresponde al `major` versión, Y es the `minor` versión, y Z la `patch` versión. Cada elemento deberá ser incremental, por ejemplo: 1.9.0 -> 1.10.0 -> 1.11.0.
2. Una vez que se ha hecho release de los cambios, ** el contenido de esa versión NO DEBE modificarse. Cualquier modificación DEBE ser lanzada como una nueva versión.**
3. La versión principal cero (0.y.z) es para el desarrollo inicial. Cualquier cosa PUEDE cambiar en cualquier momento. ** La API pública NO DEBE considerarse estable.**
4. La versión 1.0.0 define la API pública. La forma en que se incrementa el número de versión después de esta versión depende de esta API pública y de cómo cambia.
5. La versión del parche Z (x.y.z | x> 0) DEBE incrementarse si y solo si **se introducen correcciones de errores compatibles con versiones anteriores **. Una corrección de errores se define como un cambio interno que corrige un comportamiento incorrecto.
6. La versión secundaria Y (x.Y.z | x> 0) DEBE incrementarse si se introduce una nueva funcionalidad compatible con versiones anteriores en la API pública. DEBE incrementarse si alguna funcionalidad de API pública está marcada como obsoleta. PUEDE incrementarse si se introducen nuevas funciones o mejoras sustanciales dentro del código privado. PUEDE incluir cambios de nivel de parche. ** La versión del parche DEBE restablecerse a 0 cuando se incrementa la versión secundaria.**
7. La versión principal X (X.y.z | X> 0) DEBE incrementarse si ** se introducen cambios incompatibles con versiones anteriores en la API pública **. También PUEDE incluir cambios menores y de nivel de parche. ** El parche y la versión secundaria DEBEN restablecerse a 0 cuando se incrementa la versión principal. **
8. Una versión preliminar PUEDE indicarse agregando un guión y una serie de identificadores separados por puntos inmediatamente después de la versión del parche. Los identificadores DEBEN incluir sólo alfanuméricos ASCII y guión [0-9A-Za-z-]. Los identificadores NO DEBEN estar vacíos. Los identificadores numéricos NO DEBEN incluir ceros iniciales. Las versiones preliminares tienen una precedencia menor que la versión normal asociada. Una versión preliminar indica que la versión es inestable y es posible que no satisfaga los requisitos de compatibilidad previstos según lo indica su versión normal asociada. Ejemplos: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92.
9. Los metadatos del release PUEDEN indicarse agregando un signo más y una serie de identificadores separados por puntos inmediatamente después del parche o la versión preliminar. Los identificadores DEBEN incluir sólo alfanuméricos ASCII y guión [0-9A-Za-z-]. Los identificadores NO DEBEN estar vacíos. Los metadatos de compilación DEBEN ignorarse al determinar la precedencia de la versión. Por lo tanto, dos versiones que solo difieren en los metadatos de compilación tienen la misma precedencia. Ejemplos: 1.0.0-alpha + 001, 1.0.0 + 20130313144700, 1.0.0-beta + exp.sha.5114f85.
10. La precedencia se refiere a cómo se comparan las versiones entre sí cuando se ordenan. La precedencia DEBE calcularse separando la versión en identificadores principales, secundarios, de parche y de versión preliminar en ese orden (los metadatos de compilación no tienen prioridad). La precedencia está determinada por la primera diferencia al comparar cada uno de estos identificadores de izquierda a derecha de la siguiente manera: Las versiones principales, secundarias y de parche siempre se comparan numéricamente. Ejemplo: 1.0.0 <2.0.0 <2.1.0 <2.1.1. Cuando mayor, menor y parche son iguales, una versión preliminar tiene menor precedencia que una versión normal. Ejemplo: 1.0.0-alpha <1.0.0. La precedencia de dos versiones preliminares con la misma versión principal, secundaria y de parche DEBE determinarse comparando cada identificador separado por puntos de izquierda a derecha hasta que se encuentre una diferencia de la siguiente manera: los identificadores que constan de solo dígitos se comparan numéricamente y los identificadores con las letras o los guiones se comparan léxicamente en el orden de clasificación ASCII. Los identificadores numéricos siempre tienen menor precedencia que los identificadores no numéricos. Un conjunto más grande de campos de prelanzamiento tiene mayor precedencia que un conjunto más pequeño si todos los identificadores anteriores son iguales. Ejemplo: 1.0.0-alpha <1.0.0-alpha.1 <1.0.0-alpha.beta <1.0.0-beta <1.0.0-beta.2 <1.0.0-beta.11 <1.0.0- RC.1 <1.0.0.

![semver](/wiki/assets/img/semver.png)


### Changelog

En conjunto con el sistema de versiones cada proyecto debe de tener un registro de cambios (a.k.a) changelog, aquí debemos de tener una lista con los cambios ordenados cronológicamente.

Esto nos servirá para que cualquier miembro del  equipo pueda visualizar los cambios que ha tenido el proyecto en cada versión y consultar si necesita hacer algo adicional para consumir el proyecto/dependencia.

#### ¿Cómo lo hago?

- Están hechos *para los seres humanos*, no para las máquinas.
- Debe haber una entrada para cada versión.
- Los mismos tipos de cambios deben ser agrupados.
- Versiones y secciones deben ser enlazables.
- La última versión va primero.
- Debe mostrar la fecha de publicación de cada versión.
- Indicar si el proyecto sigue el [Versionamiento Semántico](https://semver.org/).
- Cada versión se escribe a manera de titulo, acompañado por la fecha del release: `[v1.5.10] - 2021-06-21`
- Mientras no se libere un release con la nueva versión, los cambios se sumen a la próxima liberación se pueden colocarse con la etiqueta: `[Unreleased]`

#### Tipos de cambios

- `Added` para funcionalidades nuevas.
- `Changed` para los cambios en las funcionalidades existentes.
- `Deprecated` para indicar que una característica o funcionalidad está obsoleta y que se eliminará en las próximas versiones.
- `Removed` para las características en desuso que se eliminaron en esta versión.
- `Fixed` para corrección de errores.
- `Security` en caso de vulnerabilidades.
- `Unreleased` para llevar los cambios que se aplicarán en el siguiente release

#### ¿Qué no debemos hacer?

- Tener información erronea o desactualizada
- Si hacemos un breaking change, debemos de estar conscientes de que la documentación debe de estar actualizada, así como una guía que explique como migrar entre versiones.

#### Ejemplo

```
# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] - 2017-06-20
### Added
- New visual identity by [@tylerfortune8](https://github.com/tylerfortune8).
- Version navigation.
- Links to latest released version in previous versions.
- "Why keep a changelog?" section.
- "Who needs a changelog?" section.
- "How do I make a changelog?" section.
- "Frequently Asked Questions" section.
- New "Guiding Principles" sub-section to "How do I make a changelog?".
- Simplified and Traditional Chinese translations from [@tianshuo](https://github.com/tianshuo).
- German translation from [@mpbzh](https://github.com/mpbzh) & [@Art4](https://github.com/Art4).
- Italian translation from [@azkidenz](https://github.com/azkidenz).
- Swedish translation from [@magol](https://github.com/magol).
- Turkish translation from [@karalamalar](https://github.com/karalamalar).
- French translation from [@zapashcanon](https://github.com/zapashcanon).
- Brazilian Portugese translation from [@Webysther](https://github.com/Webysther).
- Polish translation from [@amielucha](https://github.com/amielucha) & [@m-aciek](https://github.com/m-aciek).
- Russian translation from [@aishek](https://github.com/aishek).
- Czech translation from [@h4vry](https://github.com/h4vry).
- Slovak translation from [@jkostolansky](https://github.com/jkostolansky).
- Korean translation from [@pierceh89](https://github.com/pierceh89).
- Croatian translation from [@porx](https://github.com/porx).
- Persian translation from [@Hameds](https://github.com/Hameds).
- Ukrainian translation from [@osadchyi-s](https://github.com/osadchyi-s).

### Changed
- Start using "changelog" over "change log" since it's the common usage.
- Start versioning based on the current English version at 0.3.0 to help
translation authors keep things up-to-date.
- Rewrite "What makes unicorns cry?" section.
- Rewrite "Ignoring Deprecations" sub-section to clarify the ideal
  scenario.
- Improve "Commit log diffs" sub-section to further argument against
  them.
- Merge "Why can’t people just use a git log diff?" with "Commit log
  diffs"
- Fix typos in Simplified Chinese and Traditional Chinese translations.
- Fix typos in Brazilian Portuguese translation.
- Fix typos in Turkish translation.
- Fix typos in Czech translation.
- Fix typos in Swedish translation.
- Improve phrasing in French translation.
- Fix phrasing and spelling in German translation.

### Removed
- Section about "changelog" vs "CHANGELOG".

## [0.3.0] - 2015-12-03
### Added
- RU translation from [@aishek](https://github.com/aishek).
- pt-BR translation from [@tallesl](https://github.com/tallesl).
- es-ES translation from [@ZeliosAriex](https://github.com/ZeliosAriex).

## [0.2.0] - 2015-10-06
### Changed
- Remove exclusionary mentions of "open source" since this project can
benefit both "open" and "closed" source projects equally.

## [0.1.0] - 2015-10-06
### Added
- Answer "Should you ever rewrite a change log?".

### Changed
- Improve argument against commit logs.
- Start following [SemVer](https://semver.org) properly.

## [0.0.8] - 2015-02-17
### Changed
- Update year to match in every README example.
- Reluctantly stop making fun of Brits only, since most of the world
  writes dates in a strange way.

### Fixed
- Fix typos in recent README changes.
- Update outdated unreleased diff link.

## [0.0.7] - 2015-02-16
### Added
- Link, and make it obvious that date format is ISO 8601.

### Changed
- Clarified the section on "Is there a standard change log format?".

### Fixed
- Fix Markdown links to tag comparison URL with footnote-style links.

## [0.0.6] - 2014-12-12
### Added
- README section on "yanked" releases.

## [0.0.5] - 2014-08-09
### Added
- Markdown links to version tags on release headings.
- Unreleased section to gather unreleased changes and encourage note
keeping prior to releases.

## [0.0.4] - 2014-08-09
### Added
- Better explanation of the difference between the file ("CHANGELOG")
and its function "the change log".

### Changed
- Refer to a "change log" instead of a "CHANGELOG" throughout the site
to differentiate between the file and the purpose of the file — the
logging of changes.

### Removed
- Remove empty sections from CHANGELOG, they occupy too much space and
create too much noise in the file. People will have to assume that the
missing sections were intentionally left out because they contained no
notable changes.

## [0.0.3] - 2014-08-09
### Added
- "Why should I care?" section mentioning The Changelog podcast.

## [0.0.2] - 2014-07-10
### Added
- Explanation of the recommended reverse chronological release ordering.

## [0.0.1] - 2014-05-31
### Added
- This CHANGELOG file to hopefully serve as an evolving example of a
  standardized open source project CHANGELOG.
- CNAME file to enable GitHub Pages custom domain
- README now contains answers to common questions about CHANGELOGs
- Good examples and basic guidelines, including proper date formatting.
- Counter-examples: "What makes unicorns cry?"
```

## Fuentes
* Preston-Werner T. y Semver, C.(28 de Junio 2020). *Semantic Versioning 2.0.0*, Semver. https://semver.org/
* Lacan O. y Fortune T. C.(30 de Abril 2021). *Keep a Changelog*, Keep a Changelog. https://keepachangelog.com/en/1.0.0/