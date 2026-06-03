# Yazi
## Configuración
---
**Yazi** es un administrador de archivos moderno para la terminal, diseñado para ser extremadamente rápido y eficiente. Está escrito en Rust y funciona mediante una interfaz de texto basada en tres columnas (directorio anterior, directorio actual y vista previa).
>Se recomienda que las configuraciones basicas se debe de hacer en el archivo **.zshrc** 
>```bash
>nano ~/.zshrc
>```
>No es obligatorio abrir en `nano` sino que lo pueden cambiar los el que ustedes quieran ejecutar ejemplo: vscode = code
>

**Recomendable**
```bash
yazi() {
    local tmp="$(mktemp -t yazi-cwd.XXXXXX)"
    command yazi "$@" --cwd-file="$tmp"
    if [ -f "$tmp" ]; then
        local dir="$(cat "$tmp")"
        [ -d "$dir" ] && cd "$dir"
        rm -f "$tmp"
    fi
}
```
Esta es una función para tu shell (como Bash o Zsh) que resuelve un comportamiento clásico de los gestores de archivos de terminal: **hacer que la shell cambie al directorio donde te quedaste al cerrar Yazi**.
Luego ejecutar el siguiente codigo para aplicar los cambios
```bash
source ~/.zshrc
```
Se tiene que cerrar todas las terminales abierta para que se ejecute los cambios por completo

---