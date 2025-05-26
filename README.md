# Dockerized Databases: MongoDB, PostgreSQL y MySQL

Este repositorio proporciona una configuración de Docker Compose para ejecutar **MongoDB**, **PostgreSQL** y **MySQL** con:

- ✅ Persistencia de datos
- ✅ Credenciales seguras
- ✅ Archivos de configuración personalizados

---

## 📁 Estructura de Carpetas

/db
├── docker-compose.yml
├── .env
├── mongo/
│ └── data/ # Datos persistentes de MongoDB
├── postgres/
│ ├── data/ # Datos persistentes de PostgreSQL
│ ├── postgresql.conf # Configuración personalizada
│ └── pg_hba.conf # Reglas de acceso
├── mysql/
│ └── data/ # Datos persistentes de MySQL
└── backups/
└── postgres/ # Aquí puedes guardar los archivos .dump


---

## 🚀 Instalación y Uso

### Configurar variables de entorno

Copia el archivo `.env.example` como `.env` y define tus credenciales:

```bash
cp .env.example .env 
```

### Edita .env y coloca tus contraseñas para PostgreSQL, MySQL y MongoDB.

Levantar los contenedores
Desde la carpeta raíz (/db), ejecuta:

```bash
docker compose up -d
```

### Verificar el estado
Para confirmar que los contenedores están corriendo:

```bash
docker ps
```

### Configuración de PostgreSQL
Puedes personalizar PostgreSQL con los archivos:

postgresql.conf → Ajusta rendimiento, memoria, conexiones, etc.

pg_hba.conf → Controla quién puede conectarse y cómo.

Asegúrate de montarlos en tu docker-compose.yml así:

volumes:
- ./postgres/data:/var/lib/postgresql/data
- ./postgres/postgresql.conf:/etc/postgresql/postgresql.conf
- ./postgres/pg_hba.conf:/etc/postgresql/pg_hba.conf

Y no olvides agregar esta línea para que los use:

yaml
command: postgres -c config_file=/etc/postgresql/postgresql.conf -c hba_file=/etc/postgresql/pg_hba.conf
