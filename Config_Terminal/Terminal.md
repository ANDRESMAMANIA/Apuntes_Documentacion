# Configuración e Personalización
---
## 1: Configuración de la terminal
---
### Configuración terminal shell

Se va a cambiar el **Shell** por uno mejor ya que se usa el nativo que es **bash** y en ves de eso vamos a usar el mas completo y actualizado que es **zsh**
Instalar zsh
```bash
sudo pacman -Syu --needed zsh
```
>Lo siguiente es verificar si  se instalo correctamente
>```bash
>zsh --version
>```
>ver los **Shell** disponible con el siguiente comando:
>```bash
>cat /etc/shells 
>```

Toca cambiar de Shell (de **bash a zsh** o viceversa) con lo siguiente :
```bash
chsh -s /bin/zsh
```  
**IMPORTANTE**
El cambio se aplicara al volver a iniciar sesión o reiniciar el equipo.

**Verificar** :
```bash
echo $SHELL
```
**Primer inicio de zsh**
Abrir terminal y ejecutar el comando:
```bash
zsh-newuser-install
```
Puedes
* configurar basico
* o elegir
	 * 0 > crear **`.zshrc`** vacío
---
**Consejo sugerido**
>Instalar plugin oficial para el **`shell Zsh`**. 
>**zsh-autosuggestions**
>Su función es sugerir de forma automática comandos basados en el historial de tu terminal mientras vas escribiendo, de una manera muy similar a como lo hace la barra de búsqueda de Google o la terminal de la base de datos de **"Fish shell"**
>>```bash
>>sudo pacman -S zsh-autosuggestions
>>```
>
>**zsh-syntax-highlighting**.
> es un complemento o _plugin_ diseñado específicamente para el intérprete de comandos Zsh (Z shell). Su función principal es proporcionar resaltado de sintaxis en tiempo real directamente en la línea de comandos mientras el usuario escribe, emulando la experiencia visual que ofrecen los editores de código modernos o entornos de desarrollo (IDEs).
> >```bash
> >sudo pacman -S zsh-syntax-highlighting
> >```  
> 
> **Activar los plugin**
> En `.zshrc`:
> >```bash
> >source /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
> >source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax highlighting.zsh
> >```
>
>**IMPORTANTE:**
>`syntax-highlighting` debe ir casi al final del archivo.

---
### Entorno Terminal shell **(zsh)**
**Framework** (Modificar entorno de zsh)

 #### **Oh My Zsh**
Instalación simple:
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Luego si gustan se puede instalar un theme 
**Recomendable** 
#### **Powerlevel10k**
> Optimizado y muy rápido que muchos temas viejos.
> Comando para **Arch Linux**
>>```bash
>>yay -S --noconfirm zsh-theme-powerlevel10k-git
>>```
>
> Comando para configurar `.zshrc`:
> >```bash
> >source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme
> >```
> .
>  Lo habitual es entrar `.zshrc` y buscar y ejecutar este codigo:
>  > ```bash
>  > ZSH_THEME=""
>  > ```
>  
>  Esto se hace cuando se instalo mediante yay no es necesario introducir el **`zsh_theme`** ya que el **`source`** que se esta implementando lo hace automáticamente. 

