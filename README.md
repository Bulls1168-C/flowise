# 🚀 Flowise – Grupo 1 (Municipio de Quito)

Bienvenido al repositorio del proyecto **Flowise**, desarrollado por el **Grupo 1 del Municipio de Quito**.  
Este proyecto forma parte del **Trabajo Final: Despliegue de entornos de automatización con n8n y Flowise integrados con PostgreSQL en Docker Compose**.

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

1️⃣ **Clonar el repositorio:**

```bash
git clone https://github.com/panivinux/flowise.git
cd flowise

2️⃣ Configurar variables de entorno (opcional):
export FLOWISE_USERNAME=admin
export FLOWISE_PASSWORD=Adm1n!2025#
export DATABASE_USER=flowise_user
export DATABASE_PASSWORD=flowise_pass
export DATABASE_NAME=flowise_db

3️⃣ Levantar los servicios con Docker Compose:
docker compose up -d

4️⃣ Acceder a la aplicación:
http://localhost:3000

🔑 Credenciales iniciales (solo para el primer arranque)
| Usuario | Contraseña  |
| ------- | ----------- |
| admin   | Adm1n!2025# |

🖥️ Configuración de dominio local
Para acceder a Flowise mediante https://iaflujos.quito.gob.ec

1️⃣ Obtener la IP del Gateway del contenedor flowise:
docker inspect -f '{{range .NetworkSettings.Networks}}{{.Gateway}}{{end}}' flowise

2️⃣ Editar /etc/hosts como superusuario:
sudo nano /etc/hosts
Agregar al final:
<IP_DEL_GATEWAY> iaflujos.quito.gob.ec

3️⃣ Verificar resolución del dominio:
ping iaflujos.quito.gob.ec

📦 Estructura del proyecto
flowise/
├── app/                # Código fuente de la aplicación
├── certs/              # Certificados SSL
├── docker-compose.yml  # Configuración de Docker Compose
├── README.md           # Documentación del proyecto
└── .env.example        # Variables de entorno de ejemplo

📝 Uso básico
Inicia sesión con las credenciales iniciales.

Crea y gestiona flujos de trabajo en Flowise.

Conecta tus APIs y modelos de IA según tu proyecto.

⚠️ Seguridad
Nunca subir archivos de claves privadas o certificados (.key, .pem) a repositorios públicos.

Cambia las credenciales iniciales después del primer arranque.












