# 📌 Guía paso a paso para ejecutar Ubuntu Backup Script

## 🛠️ Paso 1: Abrir la terminal
### 📍 Dónde hacerlo:
Abre la aplicación Terminal en Ubuntu. Puedes hacerlo presionando `Ctrl + Alt + T` o buscándola en el menú de aplicaciones.

---

## 💂️ Paso 2: Crear la carpeta `scripts` en tu home
### 📍 Dónde hacerlo:
En la terminal.

### 📌 Comando a ejecutar:
```bash
mkdir -p ~/scripts
```
### ✅ Verificación:
Ejecuta `ls ~` y asegúrate de que aparece la carpeta `scripts`.

---

## 📝 Paso 3: Crear el archivo `excluir.txt`
### 📍 Dónde hacerlo:
En la terminal dentro de `scripts`.

### 📌 Comando a ejecutar:
```bash
ls -A ~/.config | grep -E '^[aeiouAEIOU]' > ~/scripts/excluir.txt
```
### ✅ Verificación:
Abre el archivo con `cat ~/scripts/excluir.txt` y revisa si hay nombres de archivos que empiezan con vocal.

---

## 💁 Paso 4: Crear la carpeta `backup`
### 📍 Dónde hacerlo:
En la terminal.

### 📌 Comando a ejecutar:
```bash
mkdir -p ~/backup
```
### ✅ Verificación:
Ejecuta `ls ~` y confirma que la carpeta `backup` está creada.

---

## 📌 Paso 5: Crear el script y darle permisos de ejecución
### 📍 Dónde hacerlo:
Dentro de `scripts`.

### 📌 Comando para abrir un editor de texto y crear el script:
```bash
nano ~/scripts/backup.sh
```
### ✏️ Copia y pega el siguiente código en el editor nano:
```bash
#!/bin/bash

HOME_DIR="$HOME"
SCRIPTS_DIR="$HOME_DIR/scripts"
BACKUP_DIR="$HOME_DIR/backup"
CONFIG_DIR="$HOME_DIR/.config"
EXCLUDE_FILE="$SCRIPTS_DIR/excluir.txt"

if [ "$#" -ne 1 ]; then
    echo "Uso: $0 [b|r]"
    exit 1
fi

mkdir -p "$BACKUP_DIR"

if [ ! -d "$BACKUP_DIR/.git" ]; then
    git -C "$BACKUP_DIR" init
fi

backup() {
    rsync -av --exclude-from="$EXCLUDE_FILE" "$CONFIG_DIR/" "$BACKUP_DIR/"
    cd "$BACKUP_DIR" || exit
    git add .
    git commit -m "Backup: $(date '+%Y-%m-%d %H:%M:%S')"
    echo "Copia de seguridad realizada correctamente."
}

restore() {
    cp -r "$BACKUP_DIR"/* "$CONFIG_DIR/"
    echo "Restauración completada."
}

case "$1" in
    b)
        backup
        ;;
    r)
        restore
        ;;
    *)
        echo "Parámetro inválido. Usa 'b' para backup o 'r' para restaurar."
        exit 2
        ;;
esac
```
### 📌 Para guardar en nano:
1. Presiona `Ctrl + X`
2. Luego presiona `Y` (Sí)
3. Presiona `Enter` para confirmar.

### 📌 Darle permisos de ejecución:
```bash
chmod +x ~/scripts/backup.sh
```
### ✅ Verificación:
Ejecuta `ls -l ~/scripts/backup.sh` y revisa que tenga permisos de ejecución `(-rwxr-xr-x)`.

---

## 📌 Paso 6: Iniciar el repositorio Git en `backup`
### 📍 Dónde hacerlo:
En la terminal.

### 📌 Comando a ejecutar:
```bash
cd ~/backup
git init
```
### ✅ Verificación:
Ejecuta `ls -a ~/backup` y asegúrate de que aparece la carpeta `.git`.

---

## 📌 Paso 7: Hacer una copia de seguridad
### 📍 Dónde hacerlo:
En la terminal.

### 📌 Comando a ejecutar:
```bash
~/scripts/backup.sh b
```
### ✅ Verificación:
- Ejecuta `ls ~/backup` y asegúrate de que los archivos de `.config` están allí.
- Ejecuta `git log --oneline` dentro de `backup` para ver el commit registrado.

---

## 📌 Paso 8: Restaurar la copia de seguridad
### 📍 Dónde hacerlo:
En la terminal.

### 📌 Comando a ejecutar:
```bash
~/scripts/backup.sh r
```
### ✅ Verificación:
Los archivos de `.config` deberían restaurarse desde `backup`.

---

## 📌 Paso 9: Probar con parámetros incorrectos
### 📍 Dónde hacerlo:
En la terminal.

### 📌 Comando a ejecutar:
```bash
~/scripts/backup.sh x
```
### ✅ Resultado esperado:
El script debe mostrar: `Parámetro inválido. Usa 'b' para backup o 'r' para restaurar.`

---

## 🎯 Conclusión
Siguiendo esta guía, has aprendido a:
✅ Crear carpetas y archivos en Ubuntu.
✅ Usar comandos básicos como `mkdir`, `ls`, `grep`, `chmod`, `cp`, `rsync` y `git`.
✅ Hacer un script en Bash con automatización.
✅ Crear un sistema de copia de seguridad con control de versiones en Git.

🚀 ¡Ya tienes un script funcional para hacer copias de seguridad de archivos en Ubuntu!

