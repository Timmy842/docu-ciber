El comando **`find`** se usa para **buscar archivos y directorios** en un sistema Linux según distintos **criterios** (nombre, tipo, tamaño, propietario, fecha, permisos, etc.).

Permite **acciones automáticas** sobre los resultados (como borrar, mover o ejecutar comandos).

---

### ⚙️ Sintaxis básica

`find [ruta] [opciones] [expresión]`

- `ruta` → carpeta donde inicia la búsqueda (ej. `/home`, `/`, `.`)

- `opciones / expresión` → condiciones o filtros de búsqueda

---

### 🔍 Ejemplos comunes

#### Buscar por nombre

`find /home -name "archivo.txt"`

🔸 Busca un archivo específico (sensible a mayúsculas).

`find /home -iname "archivo.txt"`

🔸 Ignora mayúsculas/minúsculas.

---

#### Buscar por tipo

`find /etc -type d     # Directorios find /var -type f     # Archivos normales`

Tipos comunes:

- `f`: archivo

- `d`: directorio

- `l`: enlace simbólico


---

#### Buscar por tamaño

`find / -size +100M`

🔸 Archivos mayores a **100 MB**.  
(Otros sufijos: `k`, `M`, `G`)

---

#### Buscar por fecha

`find /home -mtime -7`

🔸 Archivos **modificados hace menos de 7 días**.

- `-mtime n`: días desde última modificación

- `-atime n`: acceso

- `-ctime n`: cambio de metadatos

---

#### Buscar por permisos o propietario

`find /var/www -user carlos find /etc -perm 644`

---

#### Buscar y ejecutar una acción

`find /tmp -name "*.log" -exec rm {} \;`

🔸 Elimina todos los `.log` encontrados.  
`{}` representa el archivo encontrado.

---

### ⚡ Opciones útiles

|Opción|Descripción|
|---|---|
|`-maxdepth n`|Limita la profundidad de búsqueda|
|`-mindepth n`|Empieza a buscar a partir de cierta profundidad|
|`-empty`|Encuentra archivos o carpetas vacíos|
|`-not` o `!`|Niega una condición|
|`-o`|“OR” lógico (permite combinar filtros)|

Ejemplo:

`find /home \( -name "*.jpg" -o -name "*.png" \)`

🔸 Busca imágenes `.jpg` **o** `.png`.

---

### 💡 Diferencias con `locate`

- **`find`** → busca en tiempo real en el sistema de archivos.

- **`locate`** → usa una base de datos indexada (más rápido, pero no siempre actualizada).  

---

### 🧠 Tip práctico

Para evitar errores de permisos:

`sudo find / -name "archivo.txt" 2>/dev/null`

🔸 Redirige los mensajes de error al vacío.