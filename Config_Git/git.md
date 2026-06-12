cat << 'EOF' > git-reference.md

# Git Cheat Sheet (Referencia Rápida)

Guía rápida de comandos de Git basada en [quickref.me/git](https://quickref.me/git).

## Configuración

Configura la información del usuario para todos los repositorios locales.

| Comando                                    | Descripción                      |
| :----------------------------------------- | :------------------------------- |
| `git config --global user.name "[nombre]"` | Establece el nombre de usuario   |
| `git config --global user.email "[email]"` | Establece el correo electrónico  |
| `git config --global color.ui auto`        | Colorea la salida de la terminal |
| `git config --list`                        | Muestra la configuración actual  |

## Crear Repositorios

Inicia un nuevo repositorio o clona uno existente.

| Comando                      | Descripción                                  |
| :--------------------------- | :------------------------------------------- |
| `git init [nombre-proyecto]` | Crea un nuevo repo local                     |
| `git clone [url]`            | Descarga un proyecto y su historial completo |

## Realizar Cambios

Revisa el estado y registra los cambios (staging & commit).

| Comando                        | Descripción                                              |
| :----------------------------- | :------------------------------------------------------- |
| `git status`                   | Muestra archivos modificados en el directorio            |
| `git add [archivo]`            | Añade un archivo al área de preparación (staging)        |
| `git add .`                    | Añade todos los cambios al staging                       |
| `git commit -m "[mensaje]"`    | Registra el snapshot de los archivos de forma permanente |
| `git commit -a -m "[mensaje]"` | Añade todos los archivos rastreados y hace commit        |
| `git diff`                     | Muestra diferencias de archivos no preparados            |
| `git diff --staged`            | Muestra diferencias entre staging y la última versión    |

## Ramas (Branches)

Trabaja con ramas para aislar el desarrollo.

| Comando                       | Descripción                                |
| :---------------------------- | :----------------------------------------- |
| `git branch`                  | Lista las ramas locales                    |
| `git branch [nombre-rama]`    | Crea una nueva rama                        |
| `git checkout [nombre-rama]`  | Cambia a la rama especificada              |
| `git switch -c [nombre-rama]` | Crea y cambia a la nueva rama              |
| `git merge [rama]`            | Combina la rama especificada con la actual |
| `git branch -d [nombre-rama]` | Borra la rama seleccionada                 |

## Actualizar y Publicar

Sincroniza tu repositorio local con el remoto (GitHub/GitLab).

| Comando                    | Descripción                                  |
| :------------------------- | :------------------------------------------- |
| `git fetch [remoto]`       | Descarga el historial del remoto             |
| `git pull`                 | Descarga el historial y fusiona los cambios  |
| `git push [remoto] [rama]` | Sube los cambios locales al remoto           |
| `git remote -v`            | Muestra las URLs de los remotos configurados |

## Deshacer Cambios

Borra o regresa a estados anteriores.

| Comando                     | Descripción                                                  |
| :-------------------------- | :----------------------------------------------------------- |
| `git reset [archivo]`       | Saca el archivo del staging pero mantiene el contenido       |
| `git checkout -- [archivo]` | Deshace los cambios en el archivo (vuelve al último commit)  |
| `git revert [commit]`       | Crea un nuevo commit que deshace los cambios de uno anterior |
| `git reset --hard [commit]` | Descarta todo el historial y cambios hasta ese commit        |

## Historial e Información

Explora la evolución del proyecto.

| Comando               | Descripción                                       |
| :-------------------- | :------------------------------------------------ |
| `git log`             | Muestra el historial de commits de la rama actual |
| `git log --oneline`   | Resumen de commits en una sola línea              |
| `git show [commit]`   | Muestra los cambios de un commit específico       |
| `git blame [archivo]` | Muestra quién cambió qué en un archivo            |

## Archivos Temporales (Stash)

Guarda cambios inacabados para trabajar en otra cosa.

| Comando          | Descripción                                              |
| :--------------- | :------------------------------------------------------- |
| `git stash`      | Almacena temporalmente los cambios modificados           |
| `git stash list` | Lista los estados guardados                              |
| `git stash pop`  | Recupera los cambios del stash y los elimina de la lista |
| `git stash drop` | Descarta los cambios del stash                           |

EOF

echo "Archivo git-reference.md creado exitosamente."
