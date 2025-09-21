# Práctica de DDL en PostgreSQL con Python

## Descripción

Este proyecto demuestra cómo realizar operaciones de definición de datos (DDL) en una base de datos PostgreSQL utilizando Python. Los ejemplos están orientados a la creación, modificación y gestión de tablas con temática de **animes** y **waifus de anime**. El flujo cubre desde la configuración del entorno hasta la manipulación de la base de datos y la inserción de datos, todo gestionado desde scripts de Python y visualizado de manera gráfica en **IntelliJ IDEA**.

---

## Requisitos Previos

- **Docker** (para ejecutar PostgreSQL)
- **Python 3.13** o superior
- **pip** (gestor de paquetes de Python)
- **psycopg2** (`pip install psycopg2`)
- **IntelliJ IDEA** (con el plugin de Python y Database)
- (Opcional) Puedes utilizar **PyCharm**, **VS Code**, **DataGrip**, **DBeaver** o **pgAdmin** como alternativas para trabajar con bases de datos y código Python.

---


## Levantar PostgreSQL con Docker

Lanza tu contenedor PostgreSQL con:

```sh
docker run --name Contenedor1 -e POSTGRES_USER=Mayro -e POSTGRES_PASSWORD=Robin1710 -p 5432:5432 -d postgres
```
**Usuario y datos de Conexion puedes ser diferentes de acorde al Usuario**
- **Usuario:** Mayro
- **Contraseña:** Robin1710
- **Puerto:** 5432
- **Base de datos:** postgres

---

## Configuración de la Conexión en Python

Usa este bloque para conectar tus scripts:

```python
import psycopg2

conn = psycopg2.connect(
    host="localhost",
    port=5432,
    database="postgres",
    user="Mayro",
    password="Robin1710"
)
cur = conn.cursor()
# ... operaciones aquí ...
cur.close()
conn.close()
```

---

## Scripts Incluidos

### 1. Crear Tablas (`CrearTablas.py`)
Crea las tablas `animes` y `waifus`:

```python
cur.execute("""
    CREATE TABLE IF NOT EXISTS animes (
        id SERIAL PRIMARY KEY,
        nombre_anime VARCHAR(100)
    );
""")
cur.execute("""
    CREATE TABLE IF NOT EXISTS waifus (
        id SERIAL PRIMARY KEY,
        nombre_waifu VARCHAR(100)
    );
""")
```

### 2. Agregar Columnas (`AgregarColumna.py`)
```python
cur.execute("ALTER TABLE animes ADD COLUMN año_estreno INTEGER;")
cur.execute("ALTER TABLE waifus ADD COLUMN anime_origen VARCHAR(100);")
```

### 3. Renombrar Columnas (`RenombrarColumna.py`)
```python
cur.execute("ALTER TABLE waifus RENAME COLUMN nombre_waifu TO waifu;")
```

### 4. Eliminar Columnas (`EliminarColumna.py`)
```python
cur.execute("ALTER TABLE animes DROP COLUMN año_estreno;")
```

### 5. Agregar Restricción CHECK (`AgregarCheck.py`)
```python
cur.execute("ALTER TABLE waifus ADD CONSTRAINT check_nombre CHECK (char_length(waifu) > 2);")
```

### 6. Eliminar una Tabla (`EliminarTabla.py`)
```python
cur.execute("DROP TABLE IF EXISTS animes;")
```

### 7. Insertar Datos desde Consola (`InsertarWaifuPorConsola.py`)
```python
waifu = input("Nombre de la waifu: ")
anime = input("Anime de origen: ")
cur.execute("INSERT INTO waifus (waifu, anime_origen) VALUES (%s, %s);", (waifu, anime))
```


### 8. Ver Columnas de una Tabla (`VerColumnas.py`)
```python
nombre_tabla = "waifus"
cur.execute("""
    SELECT column_name, data_type
    FROM information_schema.columns
    WHERE table_name = %s;
""", (nombre_tabla,))
print(f"Columnas de '{nombre_tabla}':", cur.fetchall())
```

---

## Uso en IntelliJ IDEA (o cualquier IDE)

1. Abre tu proyecto en **IntelliJ IDEA**.
2. Ejecuta cada archivo `.py` con clic derecho > **Run**.
3. Usa el panel **Database** para conectar y visualizar tus tablas gráficamente.
4. Puedes realizar inserciones por consola o desde el panel visual de la base de datos.
5. **Alternativa:** Puedes realizar el mismo flujo en **PyCharm** o **VS Code** (usando la extensión de Python y algún plugin/cliente para PostgreSQL).

---

## Notas Finales

- Siempre revisa que tu contenedor Docker esté activo antes de ejecutar los scripts.
- Puedes refrescar la vista de la base de datos en tu IDE para verificar los cambios.
- Este flujo es flexible y puedes adaptarlo a cualquier tipo de tabla o estructura que desees practicar.

---

**¡Puedes usar IntelliJ IDEA, PyCharm o VS Code para este flujo, elige el que más te guste!**

**Datos del Autor**
Nombre Completo: Mayro Geovanni Barrios Gameros
Carné: 2890-23-11428
Curso: 6to ciclo de Ingeniería en Sistemas
Correo: barriosgamerosmayro@gmail.com
