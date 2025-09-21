# 🚀 Flowise – Grupo 1 (Municipio de Quito)

Bienvenido al repositorio del proyecto **Flowise**, desarrollado por el **Grupo 1 del Municipio de Quito**.  
Este proyecto forma parte del **Trabajo Final: 
Despliegue de entornos de automatización con Flowise integrados con PostgreSQL en Docker Compose**.

---

## 👥 Integrantes

| Nombre completo | Repositorio GitHub |
|-----------------|------------------|
| Carpio Zaquinaula, Byron Orlando | https://github.com/bcarpio16/flowise.git |
| Villarroel Vera, Milton Orlando | https://github.com/movillarroel/flowise.git |
| Mena Segura, Edison Fabián | https://github.com/Bulls1168-C/flowise.git |
| Benavides Freire, Alex Vicente | https://github.com/abenavides86/flowise.git |
| Gallardo Nicolalde, Marcelo Iván | https://github.com/panivinux/flowise.git |

---

## 📄 Descripción General

El objetivo de esta parte del trabajo es desplegar **Flowise**, integrado con **PostgreSQL**, utilizando **Docker Compose**.  
Se busca aplicar conceptos de **orquestación de contenedores**, **persistencia de datos**, **separación de servicios** y **buenas prácticas** en la gestión de entornos.
Como valor agregado se ha instalado certificados autofirmados SSL y el ingreso al sistema se realizará en https://iaflujos.quito.gob.ec

---

## 🔧 Requisitos Técnicos para Flowise

1️⃣ **Infraestructura**

- Docker y Docker Compose instalados en el host.
- El contenedor de Flowise debe comunicarse a través de una **red personalizada** en Docker.
- La base de datos PostgreSQL debe tener un **volumen persistente** para guardar los datos.

2️⃣ **Servicios – Flowise + PostgreSQL**

- Flowise disponible en el **puerto 3000**.  
- Base de datos PostgreSQL dedicada e independiente de otros servicios (como n8n).  
- Uso de variables de entorno definidas en un archivo `.env`.

3️⃣ **Buenas Prácticas**

- Usar un archivo `.env` para todas las credenciales y configuraciones sensibles.  
- Mantener separación clara de servicios dentro del `docker-compose.yml`.  
- No usar bind mounts, garantizando portabilidad de la aplicación.  
- Documentar en README.md instrucciones claras para levantar y detener Flowise.

---

## ⚡ Instalación y primer arranque

### La instalación de Flowise esta configurado con certificados autofirmados SSL y su validación se realizará en esta URL https://iaflujos.quito.gob.ec, para esto seguir los siguientes pasos:

1️⃣ **Clonar el repositorio:**
```
git clone https://github.com/panivinux/flowise.git
cd flowise
```

📦 Estructura del proyecto
```
tree -a
```

```
flowise/
├── app/                  # Código fuente de la aplicación
├── certs/                # Certificados SSL
├── docker-compose.yml    # Configuración de Docker Compose
├── README.md             # Documentación del proyecto
└── .env                  # Variables de entorno de ejemplo
```

2️⃣ Detalle de docker-compose.yml
```
networks:
  flowise-net:
    driver: bridge

volumes:
  flowise_postgres_data:

services:
  # ─── PostgreSQL para Flowise ───
  flowise_postgres:
    image: postgres:15
    container_name: flowise_postgres
    environment:
      POSTGRES_USER: ${DATABASE_USER}
      POSTGRES_PASSWORD: ${DATABASE_PASSWORD}
      POSTGRES_DB: ${DATABASE_NAME}
    networks:
      - flowise-net
    ports:
      - "5432:5432"
    volumes:
      - flowise_postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

  # ─── Flowise ───
  flowise:
    image: flowiseai/flowise:latest
    container_name: flowise
    env_file:
      - .env
    depends_on:
      - flowise_postgres
    networks:
      - flowise-net
    expose:
      - "3000"
    restart: unless-stopped

  # ─── Nginx Reverse Proxy ───
  nginx:
    image: nginx:alpine
    container_name: flowise_nginx
    restart: always
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf:ro
      - ./certs:/etc/nginx/certs:ro
    depends_on:
      - flowise
    networks:
      - flowise-net
```
4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟 1️⃣1️⃣

3️⃣ Configurar variables de entorno (opcional):

Si deseas cambiar el usuario y clave, lo puedes realizar en este archivo .env de igual manera los parámetros de la base de datos:
```
nano .env 
```
```
# ─── Credenciales iniciales (solo para primer arranque) ───
FLOWISE_USERNAME=admin
FLOWISE_PASSWORD=Adm1n!2025#
# ─── Configuración de la base de datos ───
DATABASE_TYPE=postgres
DATABASE_HOST=flowise_postgres
DATABASE_PORT=5432
DATABASE_NAME=flowisedb
DATABASE_USER=flowiseusr
DATABASE_PASSWORD=DbUsr!2025#XyZ
# ─── API Keys ───
HUGGINGFACE_API_KEY=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
# ─── Puerto de la aplicación ───
PORT=3000
```

4️⃣ Levantar los servicios con Docker Compose:
```
docker compose up -d
```

🖥️ Configuración de dominio local iaflujos.quito.gob.ec

1️⃣ Obtener la IP del Gateway del contenedor flowise:
```
docker inspect -f '{{range .NetworkSettings.Networks}}{{.Gateway}}{{end}}' flowise
```

2️⃣ Editar /etc/hosts como superusuario:
```
sudo nano /etc/hosts
```
Agregar al final:
Ejemplo:
```
172.18.0.1 iaflujos.quito.gob.ec
```
Tú escribirar en el archivo hosts la IP del Gateway que salio del contendor flowise.

3️⃣ Verificar resolución del dominio:
```
ping -c4 iaflujos.quito.gob.ec
```

4️⃣ Acceder a la aplicación y configurar - "esperar hasta que levanten bien los contenedores" :
Aceptar el riesgo del certificado no seguro porque es autofirmado.

https://iaflujos.quito.gob.ec

🔑 Credenciales iniciales (solo para el primer arranque)
| Usuario | Contraseña  |
| ------- | ----------- |
| admin   | Adm1n!2025# |

<img src="https://github.com/panivinux/flowise/raw/main/img/iaflujo1.png" width="600">


📝 Uso básico
⚠️ Seguridad











