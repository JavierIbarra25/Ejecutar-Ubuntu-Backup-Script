Siguiendo los pasos que hemos en la guía, podemos hacerlo desde esta ubicación sin necesidad de cambiar de directorio. Si en algún momento necesitamos navegar a otro directorio, podemos usar el comando 'cd' seguido de la ruta deseada.

##Aquí están los pasos que he seguido:

### 1. Crear el directorio `scripts` en tu home:

```bash
mkdir ~/scripts
```
---

### 2. Crear el archivo excluir.txt con los nombres de archivos y directorios en .config que comienzan con vocal:
```bash
ls -A ~/.config | grep -E '^[aeiouAEIOU]' > ~/scripts/excluir.txt
```
---

3. Crear el script para la copia de seguridad:
``bash
nano ~/scripts/backup_script.sh
```
Luego, dentro del editor nano, puedes escribir el contenido del script que hemos discutido anteriormente.

---

4. Hacer que el script sea ejecutable:
```bash
chmod +x ~/scripts/backup_script.sh
```
5. Ejecutar el script para realizar una copia de seguridad:
```bash
~/scripts/backup_script.sh b
```
6. Ejecutar el script para restaurar una copia de seguridad:
```bash
~/scripts/backup_script.sh r
```
