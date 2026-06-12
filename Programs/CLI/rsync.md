# 📦 Guía Completa de Comandos `rsync` en Arch Linux

---

## ¿Qué es `rsync`?

`rsync` significa **Remote Sync** (Sincronización Remota). Es una herramienta de línea de comandos que permite **copiar, sincronizar y transferir archivos** tanto de forma **local** como **remota** de manera eficiente. Solo transfiere las **diferencias** entre archivos, lo que lo hace mucho más rápido que `cp`.

---

## ⚙️ SINTAXIS BASE

```bash
rsync [OPCIONES] ORIGEN DESTINO
```

---

## 📋 LISTADO COMPLETO DE COMANDOS Y OPCIONES

---

### 🟢 GRUPO 1 — Copia Básica de Archivos

---

#### 1 Copiar un archivo simple

```bash
rsync archivo.txt /ruta/destino/
```

> **¿Por qué usarlo?** Es el equivalente directo a `cp` pero con la capacidad de retomar si se interrumpe. Ideal para copias simples sin necesidad de opciones adicionales.

---

#### 2 Copiar mostrando progreso

```bash
rsync --progress archivo.txt /ruta/destino/
```

> **¿Por qué usarlo?** Muestra el progreso **por archivo individual**: bytes copiados, porcentaje, velocidad y tiempo restante. Perfecto cuando copias archivos grandes y quieres saber cuánto falta.

---

#### 3️⃣ Copiar con progreso TOTAL (todos los archivos juntos)

```bash
rsync -r --info=progress2 /origen/ /destino/
```

> **¿Por qué usarlo?** En lugar de mostrar el progreso archivo por archivo, muestra el **progreso global** de toda la operación. Ideal cuando copias cientos de archivos pequeños.

---

#### 4️⃣ Copiar un directorio completo (recursivo)

```bash
rsync -r /origen/ /destino/
```

> **¿Por qué usarlo?** La opción `-r` (recursive) permite copiar **carpetas completas** con todo su contenido interno. Sin esta opción, rsync solo copia archivos individuales.

---

#### 5️⃣ Copiar directorio preservando TODO (modo archivo)

```bash
rsync -a /origen/ /destino/
```

> **¿Por qué usarlo?** La opción `-a` (archive) es una de las más importantes. Equivale a `-rlptgoD` en un solo carácter. Preserva: permisos, fechas, propietarios, grupos, enlaces simbólicos y dispositivos especiales. Es la opción más usada en backups.

---

#### 6️⃣ Copiar con modo archivo + progreso (la combinación más usada)

```bash
rsync -ah --progress /origen/ /destino/
```

> **¿Por qué usarlo?** Combina el modo archivo completo con progreso visible y tamaños legibles por humanos (`-h`). Es la **combinación más recomendada** para uso general diario.

---

### 🟡 GRUPO 2 — Opciones de Visualización e Información

---

#### 7️⃣ Modo verbose (detallado)

```bash
rsync -v /origen/ /destino/
```

> **¿Por qué usarlo?** Muestra en pantalla **cada archivo** que está siendo procesado. Útil para saber exactamente qué está copiando rsync en tiempo real.

---

#### 8️⃣ Modo muy verbose (ultra detallado)

```bash
rsync -vv /origen/ /destino/
```

> **¿Por qué usarlo?** Muestra información **aún más detallada** que `-v`, incluyendo archivos omitidos y detalles internos del proceso. Útil para depurar problemas.

---

#### 9️⃣ Mostrar tamaños en formato humano (KB, MB, GB)

```bash
rsync -ah /origen/ /destino/
```

> **¿Por qué usarlo?** Sin `-h` los tamaños se muestran en bytes puros (difícil de leer). Con `-h` (human-readable) verás `1.5G`, `300M`, `45K`, etc.

---

#### 🔟 Simulación en seco (no copia nada, solo muestra qué haría)

```bash
rsync -avn /origen/ /destino/
```

> **¿Por qué usarlo?** La opción `-n` o `--dry-run` es **crítica antes de ejecutar comandos peligrosos**. Te muestra exactamente qué archivos serían copiados, modificados o eliminados SIN hacer ningún cambio real. Siempre úsala antes de sincronizaciones importantes.

---

#### 1️⃣1️⃣ Ver estadísticas completas al final

```bash
rsync -a --stats /origen/ /destino/
```

> **¿Por qué usarlo?** Al finalizar muestra un **resumen estadístico completo**: número de archivos transferidos, tamaño total, velocidad de transferencia, datos enviados y recibidos. Ideal para reportes de backup.

---

### 🟠 GRUPO 3 — Sincronización y Actualización

---

#### 1️⃣2️⃣ Solo copiar archivos más nuevos o que no existen en destino

```bash
rsync -au /origen/ /destino/
```

> **¿Por qué usarlo?** La opción `-u` (update) **omite archivos que ya existen en destino y son más nuevos**. Perfecto para sincronizaciones donde no quieres sobreescribir versiones más recientes.

---

#### 1️⃣3️⃣ Sincronización exacta (elimina archivos que no están en origen)

```bash
rsync -a --delete /origen/ /destino/
```

> **¿Por qué usarlo?** Hace que el destino sea un **espejo exacto** del origen. Si borras un archivo en el origen, también se borra en el destino. ⚠️ **Úsalo con cuidado**, ideal para backups espejo.

---

#### 1️⃣4️⃣ Eliminar archivos pero enviarlos a una papelera primero

```bash
rsync -a --delete --backup --backup-dir=/ruta/papelera/ /origen/ /destino/
```

> **¿Por qué usarlo?** Antes de eliminar archivos del destino, los mueve a una carpeta de respaldo. Es una versión **más segura de `--delete`** que evita pérdidas accidentales de datos.

---

#### 1️⃣5️⃣ Solo copiar archivos que hayan cambiado (por checksum)

```bash
rsync -ac /origen/ /destino/
```

> **¿Por qué usarlo?** La opción `-c` (checksum) compara los archivos mediante su **hash MD5** en lugar de solo fecha y tamaño. Más lento pero **más preciso** para detectar cambios reales en el contenido.

---

#### 1️⃣6️⃣ No sobreescribir archivos existentes en destino

```bash
rsync -a --ignore-existing /origen/ /destino/
```

> **¿Por qué usarlo?** Copia solo archivos que **NO existen en el destino**, sin tocar los que ya están ahí. Útil cuando quieres hacer una copia inicial sin alterar lo que ya hay.

---

### 🔵 GRUPO 4 — Filtros y Exclusiones

---

#### 1️⃣7️⃣ Excluir un archivo específico

```bash
rsync -a --exclude="archivo.txt" /origen/ /destino/
```

> **¿Por qué usarlo?** Permite **omitir archivos o carpetas concretas** de la copia. Muy útil cuando no quieres incluir archivos temporales o configuraciones locales.

---

#### 1️⃣8️⃣ Excluir múltiples archivos

```bash
rsync -a --exclude="*.log" --exclude="*.tmp" --exclude=".cache/" /origen/ /destino/
```

> **¿Por qué usarlo?** Puedes encadenar múltiples `--exclude` para omitir logs, temporales, cachés o cualquier patrón de archivos que no necesites respaldar.

---

#### 1️⃣9️⃣ Excluir usando un archivo de lista

```bash
rsync -a --exclude-from="exclusiones.txt" /origen/ /destino/
```

> **¿Por qué usarlo?** Si tienes muchos archivos a excluir, en lugar de escribir `--exclude` muchas veces, creas un archivo `.txt` con un patrón por línea. Mucho más organizado y reutilizable.

Ejemplo del archivo `exclusiones.txt`:

```
*.log
*.tmp
.cache/
node_modules/
.git/
```

---

#### 2️⃣0️⃣ Incluir solo ciertos tipos de archivos

```bash
rsync -a --include="*.jpg" --exclude="*" /origen/ /destino/
```

> **¿Por qué usarlo?** Primero defines qué **SÍ** quieres incluir y luego excluyes todo lo demás. En este ejemplo, solo copia archivos `.jpg`. El orden `--include` antes de `--exclude` es importante.

---

#### 2️⃣1️⃣ Excluir carpetas ocultas y archivos del sistema

```bash
rsync -a --exclude=".*" /origen/ /destino/
```

> **¿Por qué usarlo?** Omite todos los archivos y carpetas que comienzan con `.` (ocultos en Linux), como `.bashrc`, `.config`, `.git`, etc.

---

### 🟣 GRUPO 5 — Transferencias Remotas (SSH)

---

#### 2️⃣2️⃣ Copiar archivo local → servidor remoto

```bash
rsync -avh --progress archivo.txt usuario@servidor:/ruta/destino/
```

> **¿Por qué usarlo?** Transfiere archivos **desde tu máquina local hacia un servidor remoto** a través de SSH de forma segura. Más eficiente que `scp` porque solo transfiere las diferencias.

---

#### 2️⃣3️⃣ Copiar servidor remoto → local (descarga)

```bash
rsync -avh --progress usuario@servidor:/ruta/origen/ /ruta/local/
```

> **¿Por qué usarlo?** Descarga archivos o directorios desde un servidor remoto a tu máquina local. Ideal para obtener backups o sincronizar contenido desde un VPS.

---

#### 2️⃣4️⃣ Usar puerto SSH personalizado

```bash
rsync -avh -e "ssh -p 2222" /origen/ usuario@servidor:/destino/
```

> **¿Por qué usarlo?** Por defecto rsync usa el puerto SSH 22. Si tu servidor usa un **puerto diferente**, con `-e "ssh -p PUERTO"` especificas el puerto correcto.

---

#### 2️⃣5️⃣ Usar llave SSH específica para autenticación

```bash
rsync -avh -e "ssh -i ~/.ssh/mi_llave_privada" /origen/ usuario@servidor:/destino/
```

> **¿Por qué usarlo?** Si tienes múltiples llaves SSH, puedes indicar exactamente **cuál llave usar** para autenticarte en el servidor. Esencial en entornos con múltiples servidores.

---

#### 2️⃣6️⃣ Limitar el ancho de banda usado (no saturar la red)

```bash
rsync -avh --bwlimit=5000 /origen/ usuario@servidor:/destino/
```

> **¿Por qué usarlo?** Limita la velocidad de transferencia a **5000 KB/s (≈5 MB/s)**. Útil para no saturar la red mientras otros usuarios la utilizan o cuando tienes datos limitados.

---

### 🔴 GRUPO 6 — Backups Avanzados

---

#### 2️⃣7️⃣ Backup incremental con fecha

```bash
rsync -a --backup --backup-dir=/backups/$(date +%Y-%m-%d) /origen/ /destino/
```

> **¿Por qué usarlo?** Cada día crea una carpeta con la fecha actual y guarda ahí solo los archivos **que cambiaron ese día**. Sistema de backup incremental completo y automático.

---

#### 2️⃣8️⃣ Continuar transferencia interrumpida

```bash
rsync -avh --partial --progress /origen/ /destino/
```

> **¿Por qué usarlo?** Si la transferencia se corta a la mitad, `--partial` mantiene el archivo parcialmente copiado. La próxima vez que ejecutes el comando, **retoma desde donde quedó** en lugar de empezar de cero.

---

#### 2️⃣9️⃣ Modo retomar + checksum (el más seguro para reanudar)

```bash
rsync -avh --partial --append-verify /origen/ /destino/
```

> **¿Por qué usarlo?** Reanuda transferencias incompletas y además **verifica con checksum** los datos ya transferidos para garantizar integridad. El más seguro para archivos grandes críticos.

---

#### 3️⃣0️⃣ Preservar enlaces simbólicos

```bash
rsync -avhl /origen/ /destino/
```

> **¿Por qué usarlo?** La opción `-l` copia los **enlaces simbólicos tal como son** (como accesos directos) en lugar de copiar el archivo al que apuntan. Esencial para preservar la estructura real del sistema.

---

#### 3️⃣1️⃣ Copiar siguiendo los enlaces simbólicos (copiar el archivo real)

```bash
rsync -avhL /origen/ /destino/
```

> **¿Por qué usarlo?** Al contrario de `-l`, la opción `-L` **sigue los enlaces** y copia el archivo real al que apuntan. Útil cuando quieres una copia independiente sin depender de symlinks.

---

#### 3️⃣2️⃣ Preservar ACLs y atributos extendidos

```bash
rsync -aAX /origen/ /destino/
```

> **¿Por qué usarlo?** `-A` preserva las **ACLs** (listas de control de acceso) y `-X` preserva los **atributos extendidos** del sistema de archivos. Fundamental para backups completos del sistema.

---

### ⚫ GRUPO 7 — Comandos para Sistema Completo

---

#### 3️⃣3️⃣ Backup completo del sistema (excepto virtuales)

```bash
rsync -aAXvh --progress \
  --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","lost+found"} \
  / /mnt/backup/
```

> **¿Por qué usarlo?** Hace una copia completa de **todo el sistema operativo** excluyendo las carpetas virtuales del kernel que no se pueden ni deben copiar. Es el comando estándar para clonar Arch Linux.

---

#### 3️⃣4️⃣ Sincronizar dos directorios locales de forma segura

```bash
rsync -avhn --delete /origen/ /destino/
```

> **¿Por qué usarlo?** Primero ejecuta el **dry-run** (`-n`) para ver qué se borraría con `--delete` antes de hacerlo real. Siempre recomendado antes de sincronizaciones destructivas.

---

## 📊 TABLA RESUMEN DE OPCIONES CLAVE

| Opción      | Nombre             | ¿Qué hace?                                          |
| ----------- | ------------------ | --------------------------------------------------- |
| `-a`        | Archive            | Preserva todo (permisos, fechas, propietario, etc.) |
| `-v`        | Verbose            | Muestra archivos procesados                         |
| `-h`        | Human readable     | Tamaños en KB, MB, GB                               |
| `-r`        | Recursive          | Copia directorios completos                         |
| `-n`        | Dry-run            | Simula sin hacer cambios reales                     |
| `-u`        | Update             | Solo copia si el origen es más nuevo                |
| `-c`        | Checksum           | Compara por hash, no por fecha                      |
| `-z`        | Compress           | Comprime datos durante la transferencia             |
| `-P`        | Progress + Partial | Muestra progreso y permite reanudar                 |
| `-l`        | Links              | Preserva symlinks como symlinks                     |
| `-L`        | Copy Links         | Copia el archivo real del symlink                   |
| `-A`        | ACLs               | Preserva listas de control de acceso                |
| `-X`        | Extended           | Preserva atributos extendidos                       |
| `--delete`  | Eliminar           | Borra en destino lo que no está en origen           |
| `--exclude` | Excluir            | Omite archivos o patrones                           |
| `--partial` | Parcial            | Mantiene archivos de transferencias cortadas        |
| `--bwlimit` | Ancho de banda     | Limita la velocidad de transferencia                |
| `--stats`   | Estadísticas       | Muestra resumen al finalizar                        |
| `--backup`  | Respaldo           | Guarda versiones anteriores antes de sobreescribir  |

---

## 💡 COMBINACIONES MÁS RECOMENDADAS

```bash
# ✅ Copia diaria general (la más usada)
rsync -avh --progress /origen/ /destino/

# ✅ Backup seguro con borrado espejo
rsync -avh --delete --dry-run /origen/ /destino/
rsync -avh --delete /origen/ /destino/   # después de confirmar

# ✅ Transferencia remota robusta
rsync -avhzP usuario@servidor:/origen/ /destino/

# ✅ Backup completo del sistema
rsync -aAXvh --progress --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*"} / /mnt/backup/
```

> 🔑 **Regla de oro:** Siempre usa `--dry-run` (`-n`) antes de ejecutar comandos con `--delete` para evitar pérdidas de datos irreversibles.
