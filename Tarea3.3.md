Siguiendo los pasos que hemos en la guía, podemos hacerlo desde esta ubicación sin necesidad de cambiar de directorio. Si en algún momento necesitamos navegar a otro directorio, podemos usar el comando 'cd' seguido de la ruta deseada.

## Aquí están los pasos que he seguido:

### 1. Crear el directorio `scripts` en tu home:

```bash
mkdir ~/scripts
```
![Captura de pantalla 2025-03-16 185550](https://github.com/user-attachments/assets/e0a09d8c-0761-41be-b004-bd87c2f0970b)
---

### 2. Crear el archivo excluir.txt con los nombres de archivos y directorios en .config que comienzan con vocal:
```bash
ls -A ~/.config | grep -E '^[aeiouAEIOU]' > ~/scripts/excluir.txt
```
![Captura de pantalla 2025-03-16 185754](https://github.com/user-attachments/assets/d777cfe8-9c35-4805-9e0a-bbc9134efe52)

---

### 3. Crear el script para la copia de seguridad:
```bash
nano ~/scripts/backup_script.sh
```
![Captura de pantalla 2025-03-16 192648](https://github.com/user-attachments/assets/6fb65819-6d02-4dee-8593-1c685eb3a719)

Luego, dentro del editor nano, puedes escribir el contenido del script que hemos discutido anteriormente.
![Captura de pantalla 2025-03-16 190920](https://github.com/user-attachments/assets/fffe4041-3c2c-4369-ab97-2e9a3528f733)

![Captura de pantalla 2025-03-16 192612](https://github.com/user-attachments/assets/f443a91e-312c-4e33-a9b2-dfd29a318460)

---

### 4. Hacer que el script sea ejecutable:
```bash
chmod +x ~/scripts/backup_script.sh
```
![Captura de pantalla 2025-03-16 193017](https://github.com/user-attachments/assets/5d4ba78d-3c2e-473e-b3c6-d6f99e30a148)
---

### 5. Ejecutar el script para realizar una copia de seguridad:
```bash
~/scripts/backup_script.sh b
```
![Captura de pantalla 2025-03-16 194500](https://github.com/user-attachments/assets/e4b49663-1f0c-401a-9548-f6a0bf7f577c)

- Aquí he tenido errores así que vamos a revisarlos en el archivo 'backup_script.sh'

![Captura de pantalla 2025-03-16 194326](https://github.com/user-attachments/assets/a2ab6a4a-53f2-4582-b79d-58e6c733d227)

- Como se puede ver hay que corregir los iguales de los '_DIR' y el if de la línea 9. Aún así es posible que te salgan otros errores, también es posible que no tengas el git instalado, te lo pndrá en la misma terminal, así que hacemos lo siguiente:

![Captura de pantalla 2025-03-16 195757](https://github.com/user-attachments/assets/b197c77f-e967-4372-8336-26cc2b8d50c6)

- Una vez hecho esto te debe salir lo siguiente al hacer '~/scripts/backup_script.sh b'

![Captura de pantalla 2025-03-16 201258](https://github.com/user-attachments/assets/18a658fe-3670-4dc5-88b1-7314db0f7fb3)

- Necesitas crear el e-mail y contraseña, yo puse el de Cesur y mio nombre (se me olvidó hacer captura) con los siguientes comandos:
  
```bash
git config --global user.email "tu_correo@example.com"
git config --global user.name "Tu Nombre"
```
- Una vez hecho, te debe salir lo siguiente:
- 
![Captura de pantalla 2025-03-16 201547](https://github.com/user-attachments/assets/70573a7d-1c9f-405b-be60-44f616964992)

- Podemos comprobar si se ha creado el git usando los comandos de la imagen

![Captura de pantalla 2025-03-16 201754](https://github.com/user-attachments/assets/4bfeb63e-26cf-49a7-b620-0b67dcbb0a39)

---

### 6. Ejecutar el script para restaurar una copia de seguridad:
```bash
~/scripts/backup_script.sh r
```
