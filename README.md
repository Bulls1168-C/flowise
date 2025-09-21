# 📦 Curso: Despliegue de Aplicaciones con Docker  

## 🎓 Información del Curso  
- **Curso:** Despliegue de Aplicaciones con Docker  
- **Proyecto:** Trabajo final - Despliegue de Flowise  
- **Profesor:** Ing. Edison Naranjo (CEC-EPN)  
- **Fecha:** 21 de Septiembre de 2025  

---


## 👥 Integrantes - Grupo 1 (Municipio de Quito)  

| Integrante | Repositorio GitHub |
|------------|--------------------|
| Carpio Zaquinaula Byron Orlando | https://github.com/bcarpio16/flowise.git |
| Villarroel Vera Milton Orlando | https://github.com/movillarroel/flowise.git |
| Mena Segura Edison Fabián | https://github.com/Bulls1168-C/flowise.git |
| Benavides Freire Alex Vicente | https://github.com/abenavides86/flowise.git |
| Gallardo Nicolalde Marcelo Iván | https://github.com/panivinux/flowise.git |

---
# ─── Credenciales iniciales (solo para primer arranque) ───
FLOWISE_USERNAME=admin
FLOWISE_PASSWORD=Adm1n!2025#

## 📑 Proyecto – Docker Compose - Grupo 1 – Trabajo Final

### 📋 Descripción del Proyecto  
El objetivo de este trabajo es deplegar Flowise, integrado con su propia base de datos PostgreSQL, utilizando Docker Compose. Con persistencia de datos, separación de servicios y buenas prácticas en la gestión del entorno.

### 📋 Requerimientos Técnicos
1. Infraestructura
   Docker Compose instalado en el host
   Los contenedores deben comunicarse a través de una rede personalizada de Docker.
   Cada servicio debe contar con un volumen persistente para su base de datos.

2. Servicios
   Base de datos PostgreSQL dedicada con credenciales seguras.
   Uso de variables de entorno definidas en un archivo .env.

   b) Flowise + PostgreSQL
◦ Flowise debe estar disponible en el puerto 3000.
◦ Base de datos PostgreSQL dedicada e independiente de la usada por n8n.
◦ Uso de variables de entorno definidas en un archivo .env.
3. Buenas Prácticas
◦ Usar un archivo .env para todas las credenciales y configuraciones sensibles.
◦ Separación clara de servicios dentro del docker-compose.yml.
◦ No usar bind mounts ya que se requiere que la aplicación sea portable.
◦ Redactar un README.md con instrucciones claras para levantar y detener los servicios.
Entregables
1. Repositorio en GitHub con:
◦ docker-compose.yml (creado desde cero por el estudiante).
◦ .env (archivo de credenciales).
◦ README.md con:
▪ Requisitos previos.
▪ Pasos para ejecutar el proyecto.
▪ Pruebas para verificar el correcto funcionamiento.
2. Pruebas de Funcionamiento
◦ Acceso al panel web de n8n en http://localhost:5678.
◦ Acceso al panel web de Flowise en http://localhost:300
   

Este proyecto implementa una aplicación web utilizando **Docker Compose** para gestionar múltiples contenedores que trabajan conjuntamente.  

La solución incluye:  
- Un **servidor web Apache con PHP**  
- Una **base de datos MariaDB**  

Esto proporciona un entorno completo para el desarrollo y despliegue de aplicaciones web.  

---
