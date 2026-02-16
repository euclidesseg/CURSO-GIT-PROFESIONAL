# 📘 Guía práctica de Git y Gitflow
_De básico a avanzado_

Esta guía organiza los comandos más importantes de Git desde los más básicos hasta los más avanzados,
e incluye un flujo Gitflow profesional para trabajo individual o en equipo.

================================================================================

``` bash
1️⃣ COMANDOS BÁSICOS DEL SISTEMA
touch historico.txt
→ Crea un archivo vacío en el directorio actual.

code historico.txt
→ Abre el archivo en Visual Studio Code.

================================================================================

2️⃣ CONFIGURACIÓN INICIAL DE GIT (SOLO UNA VEZ)

git config --global user.name "Euclides Perez"
→ Configura el nombre del usuario que aparecerá en los commits.

git config --global user.email "eperez@intecol.com.co"
→ Configura el correo electrónico asociado a los commits.

git config --global credential.helper store
→ Guarda las credenciales para no autenticarse cada vez.

================================================================================

3️⃣ FLUJO BÁSICO DE TRABAJO CON GIT

git status
→ Muestra el estado de los archivos (modificados, preparados, no rastreados).

git add historico.txt
→ Agrega un archivo específico al área de preparación (staging).

git add .
→ Agrega todos los cambios al staging.

git commit -m "Primer commit"
→ Guarda los cambios preparados en el repositorio local.

git commit -a -m "Commit rápido"
→ Agrega y commitea automáticamente archivos ya rastreados.

================================================================================

4️⃣ ENVIAR CAMBIOS AL REPOSITORIO REMOTO (MUY IMPORTANTE)

git push
→ Envía los commits locales al repositorio remoto de la rama actual.

git push origin main
→ Envía los commits de la rama main al repositorio remoto.

git push origin develop
→ Envía los commits de la rama develop al repositorio remoto.

git push -u origin nueva_rama
→ Sube una rama nueva al repositorio remoto y la vincula (tracking).

git push --force
→ Fuerza el envío de commits (⚠️ usar solo en ramas locales o controladas).

================================================================================

5️⃣ VER HISTORIAL Y CAMBIOS

git log
→ Muestra el historial completo de commits.

git log --graph --oneline --all
→ Muestra el historial resumido con ramas y gráfico visual.

git log historico.txt
→ Muestra el historial de cambios de un archivo específico.

git show
→ Muestra información detallada del último commit.

git log -p
→ Muestra los cambios línea por línea en cada commit.

git diff
→ Muestra diferencias entre el directorio de trabajo y el staging.

git diff --staged
→ Muestra diferencias entre el staging y el último commit.

================================================================================

6️⃣ MANEJO AVANZADO DEL STAGING Y ARCHIVOS

git add -p
→ Permite agregar cambios de forma interactiva (por bloques o líneas).

git restore historico.txt
→ Descarta los cambios locales antes de hacer git add.

git rm historico.txt
→ Elimina un archivo del repositorio y del sistema.

git rm --cached historico.txt
→ Elimina el archivo del staging pero lo conserva localmente.

git mv archivo_actual nuevo_nombre
→ Mueve o renombra archivos manteniendo el seguimiento de Git.

git clean -fd
→ Elimina archivos y carpetas no rastreados.

================================================================================

7️⃣ RECUPERACIÓN Y MANIPULACIÓN DEL HISTORIAL (USAR CON CUIDADO)

git reset --soft ID_COMMIT
→ Vuelve a un commit anterior manteniendo los cambios en staging.

git reset --hard ID_COMMIT
→ Vuelve a un commit anterior eliminando todos los cambios posteriores.

git checkout ID_COMMIT
→ Se mueve a un commit específico sin borrar el historial.

git reflog
→ Muestra el historial completo, incluso commits eliminados.

git revert ID_COMMIT
→ Revierte un commit creando uno nuevo (seguro para producción).

================================================================================

8️⃣ TRABAJO CON RAMAS (FUNDAMENTOS)

git branch
→ Lista todas las ramas locales.

git branch nombre_rama
→ Crea una nueva rama.

git checkout nombre_rama
→ Cambia a otra rama.

git checkout -b nueva_rama
→ Crea una nueva rama y se mueve a ella automáticamente.

git branch -D nombre_rama
→ Elimina una rama local.

git push -u origin nombre_rama
→ Envia una rama que esta en local hasta rel repositorio remoto.
================================================================================

9️⃣ FUSIÓN DE RAMAS

git merge feature1
→ Fusiona la rama feature1 en la rama actual.

git merge --abort
→ Cancela una fusión cuando hay conflictos.

Regla importante:
Primero debes posicionarte en la rama destino y luego ejecutar el merge.

================================================================================

🚀 GITFLOW (FLUJO PROFESIONAL)

================================================================================

🌱 RAMAS PRINCIPALES

main (o master)
→ Rama de producción. Contiene solo código estable.

develop
→ Rama de integración. Aquí se unen todas las funcionalidades.

================================================================================

✨ RAMAS FEATURE

Características:
- Se crean desde develop
- Contienen una sola funcionalidad
- Nunca se fusionan directamente con main

Crear una rama feature:

git checkout develop
git checkout -b feature/nueva-funcionalidad

Finalizar una feature:

git checkout develop
git merge feature/nueva-funcionalidad
git branch -d feature/nueva-funcionalidad

git push origin develop
→ Publica los cambios integrados en develop.

================================================================================

📦 RAMAS RELEASE

Características:
- Se crean desde develop
- Solo permiten correcciones, documentación y ajustes finales

Crear una release:

git checkout develop
git checkout -b release/1.0.0

Finalizar una release:

git checkout main
git merge release/1.0.0
git push origin main

git checkout develop
git merge release/1.0.0
git push origin develop

git branch -d release/1.0.0

================================================================================

🚑 RAMAS HOTFIX

Características:
- Se crean desde main
- Corrigen errores críticos en producción

Crear un hotfix:

git checkout main
git checkout -b hotfix/error-critico

Finalizar un hotfix:

git checkout main
git merge hotfix/error-critico
git push origin main

git checkout develop
git merge hotfix/error-critico
git push origin develop

git branch -d hotfix/error-critico

================================================================================

🧠 RESUMEN GITFLOW

1. main → Producción
2. develop → Integración
3. feature/* → Nuevas funcionalidades
4. release/* → Preparación de versión
5. hotfix/* → Correcciones urgentes

================================================================================

✅ BUENAS PRÁCTICAS

- Usa git reset solo en ramas locales
- Usa git revert en ramas compartidas o producción
- Evita git push --force en ramas compartidas
- Haz commits pequeños y descriptivos
- Mantén el historial limpio y legible
