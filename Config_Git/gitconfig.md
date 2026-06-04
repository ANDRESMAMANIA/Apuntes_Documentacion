# **.GitConfig**

## Tipos de configuracion

---

---

### **Configuracion mediante la terminal**

Comensemos con lo basico que son el usuario y email.

---

**Usuario:**

```bash
git config --global user.name "Tu Nombre y Apellido"
```

---

**Email:**

```bash
git config --global user.email "tu_correo@dominio.com"
```

---

Continuando comensamos con lo de dar prioridad a un **IDE** (editor de codigo)

> Va hacer el editor por defecto para los commits

```bash
git config --global core.editor "code --wait"
```

---

Permite crear un archivo `.gitignore_global` en la carpeta **usuario** en caso que no vea se tiene que crear dicho archivo.

Aqui es donde se define los archivos que se quiere ignorar en todos los proyectos que se este trabajando haciendolo universal para no estar repitiendo en cada proyecto. En el equipo que se este trabajando.

```bash
git config --global core.excludesfile "~/.gitignore_global"
```

---

Desactivar el paguinador de Git

```bash
git config --global core.pager ""
```

> Por defecto, Git usa un paguinador (normalmente `less`) cuando ejecutar comandos como:
>
> ```bash
> git log
> git diff
> ```
>
> Esto hace que la salida se muestre páguina por páguina.
> Con esta configuración
>
> - Git mostrará todo el contenido directamente en la terminal.
> - No entrará en modo paginado.
> - No tendrás que presionar `q` para salir

---

Manejo de **Salto en Linea** `(CRLF vs LF)`  
**`Linux o MacOS`**

```bash
git config --global core.autocrlf input
```

> Este comando le dice a Git como debe manejar los **`saltos de línea`**  
> (lo que ocurre cuando presionas la tecla **Enter** en tu codigo) para evitar problemas cuando trabajas en equipo con personas que usan diferentes sistemas operativos:  
> En resumen esta configuracion recomendada si usas **`MacOS o Linux`**
>
> En caso controrio si se usa **`Windows`** el comando correcto sería:
>
> ```bash
> git config --global core.autocrlf true
> ```

---

.Se establece **`Main`** como la rama por defecto al iniciar nuevos repositorios

```bash
git config --global init.defaultBranch Main
```

**Recomendable**:

> No usar como **`Master`** en la rama principal

---

**`Color.ui`**: activa y desactiva los colores en la interfaz de la terminal (true o false)

```bash
git config --global color.ui true
```

---

Configuracion GIt Pull

```bash
git config --global pull.rebase false
```

> - Cuando configuras `pull.rebase false`, le estás diciendo a Git que utilice la estrategia de Merge (Fusión) de forma obligatoria y predeterminada.
> - `git config --global pull`.rebase true: En lugar de crear un commit de fusión, Git tomaría tus commits locales, los guardaría temporalmente, aplicaría los commits remotos y luego reescribiría tus commits justo encima de los nuevos.

---

Configuración Git Push

```bash
git config --global push.default simple
```

> La configuración simple adopta un enfoque conservador para evitar que subas cambios a ramas equivocadas por accidente. Para que el comando git push funcione bajo esta modalidad, se deben cumplir dos condiciones estrictas:
>
> - Coincidencia de nombre: La rama local en la que estás parado debe llamarse exactamente igual que la rama en el repositorio remoto.
> - Rama de seguimiento (Upstream): La rama local debe estar configurada para rastrear a esa rama remota específica.

---

Configuracion **Cache**

El comando **(credential.helper cache)** levanta un proceso en segundo plano en Linux que retiene las credenciales en la memoria RAM. Al pasar los 15 minutos (o el tiempo que configures), ese proceso se destruye y la memoria se libera, obligándote a escribir la contraseña o el token de nuevo.

_**`Linux`**_

```bash
git config --global credential.helper cache
```

_**`MacOS`**_

```bash
git config --global credential.helper osxkeychain
```

_**`Windows`**_

```bash
git config --global credential.helper manager
```

---

Verificación de la configuración

```bash
git config --list --global
```

---

---

### **Configuracion mediante un IDE**

Comando para que Git de prioridad a un IDE ya sea su editor principal

```bash
git config --global core.editor "code --wait"
```

Luego comienza con la modificación de **.gitconfig** y se accede mediante el siguiente comando:

```bash
git config --global -e
```

Esto abrirá una ventana dentro de la IDE ya preestablecida

**Importartante**:

> Copiar lo siguiente que esta dentro del [archivo](gitconfig.txt)

Dentro del archivo tienes que configurar con tus datos personales y guardar.

---

---
