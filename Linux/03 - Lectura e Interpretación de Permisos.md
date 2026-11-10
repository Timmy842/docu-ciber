En Linux, **cada archivo y directorio** tiene un conjunto de permisos que determinan **quién puede leerlo, modificarlo o ejecutarlo**.  
Estos permisos se pueden ver con el comando:

`ls -l`

Por ejemplo:

`-rwxr-xr--`

---

### 📖 1. Estructura general

Cada archivo tiene **10 caracteres** de información de permisos:

|Posición|Significado|Ejemplo|Descripción|
|---|---|---|---|
|1|Tipo de archivo|`-`|`-` = archivo normal, `d` = directorio, `l` = enlace simbólico|
|2–4|Permisos del **usuario propietario**|`rwx`|Lectura, escritura y ejecución del dueño|
|5–7|Permisos del **grupo**|`r-x`|Lectura y ejecución, sin escritura|
|8–10|Permisos de **otros (resto de usuarios)**|`r--`|Solo lectura|

---

### 🧩 2. Tipos de permisos

|Símbolo|Nombre|Significado en archivos|Significado en directorios|
|---|---|---|---|
|`r`|**read (lectura)**|Permite ver el contenido|Permite listar el contenido|
|`w`|**write (escritura)**|Permite modificar o borrar|Permite crear o borrar archivos dentro|
|`x`|**execute (ejecución)**|Permite ejecutar el archivo como programa|Permite acceder dentro del directorio (`cd`)|

---

### 🧮 3. Representación numérica (modo octal)

Cada permiso tiene un valor numérico:

|Permiso|Valor|
|---|---|
|`r`|4|
|`w`|2|
|`x`|1|

Se suman para obtener un número por cada grupo:

|Tipo|Permisos|Valor|
|---|---|---|
|Usuario|rwx|4 + 2 + 1 = **7**|
|Grupo|r-x|4 + 0 + 1 = **5**|
|Otros|r--|4 + 0 + 0 = **4**|

➡️ El permiso total sería **`754`**, que equivale a `rwxr-xr--`.

---

### ⚙️ 4. Cómo cambiar permisos

Usamos el comando `chmod`:

`chmod 754 archivo.txt`

O con la forma simbólica:

`chmod u=rwx,g=rx,o=r archivo.txt`

---

### 👤 5. Propietario y grupo

Cada archivo también tiene un **dueño (usuario)** y un **grupo** asociado.  
Puedes verlos con:

`ls -l`

Ejemplo:

`-rwxr-xr--  1 carlos  devs  2048 oct 25 09:00 script.sh`

Aquí:

- **carlos** → usuario propietario
    
- **devs** → grupo al que pertenece
    
- **2048** → tamaño del archivo en bytes
    
- **oct 25 09:00** → fecha de modificación
    

Cambiar propietario o grupo:

`chown carlos:devs archivo.txt`

---

### 🧠 6. Casos comunes

|Código|Permisos|Uso típico|
|---|---|---|
|`777`|Todos pueden leer, escribir y ejecutar|No recomendable (inseguro)|
|`755`|Usuario total, grupo y otros pueden leer y ejecutar|Programas o scripts|
|`644`|Usuario puede escribir, otros solo leer|Archivos de texto|
|`700`|Solo el usuario puede acceder|Archivos privados|

---

### 🧩 Ejemplo completo

`drwxr-x---`

- `d` → es un **directorio**
    
- Usuario: `rwx` → puede leer, escribir y entrar
    
- Grupo: `r-x` → puede listar e ingresar pero no modificar
    
- Otros: `---` → no tienen ningún acceso