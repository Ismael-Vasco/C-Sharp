# 🚀 Despliegue de NGINX Proxy Manager con Docker Compose

![NGINX Proxy Manager](https://cursosdedesarrollo.com/wp-content/uploads/2022/01/logo-npm.png)

### url reference:
``https://www.youtube.com/watch?v=MlLjBt6hLHs``
## 📌 ¿Qué es NGINX Proxy Manager?

**NGINX Proxy Manager** es una herramienta basada en Docker para administrar fácilmente proxies reversos con una interfaz web. Permite:

- Redirigir tráfico a múltiples servicios internos con **dominios personalizados**.
- Gestionar **certificados SSL** de Let's Encrypt con renovación automática.
- Controlar redirecciones, accesos y más, todo sin tocar configuraciones manuales de NGINX.

Ideal para quienes gestionan varios contenedores o servicios web en un mismo servidor.

---

## 🧰 ¿Qué contiene este repositorio?

Este `docker-compose.yml` despliega:

- `jc21/nginx-proxy-manager`: la aplicación principal.
- `jc21/mariadb-aria`: base de datos MariaDB compatible.
- Persistencia de datos y certificados.
- Uso de red externa (`general-net`) para integrarse con otros contenedores.

---

## ⚙️ Cómo usar

### 1. Crea un archivo `.env` con tus variables:
```env
DB_MYSQL_HOST=db
DB_MYSQL_PORT=3306
DB_MYSQL_USER=nginx
DB_MYSQL_PASSWORD=tu_password_segura
DB_MYSQL_NAME=nginx_db
DB_MYSQL_ROOT_PASSWORD=otra_password_segura
```

### 2. Asegúrate de tener creada la red externa:

```bash
docker network create general-net
```

### 3. Inicia el stack:

```bash
docker-compose up -d
```

## 📁 Estructura de volúmenes

| Carpeta         | Propósito                                  |
| --------------- | ------------------------------------------ |
| `./data`        | Datos de configuración de NPM              |
| `./letsencrypt` | Certificados SSL                           |
| `./mysql`       | Base de datos MariaDB (datos persistentes) |

---

## ✅ Credenciales por defecto 👉 <a href="https://nginxproxymanager.com/setup/#default-administrator-user" target="_blank" rel="noopener noreferrer">Guía oficial de instalación</a>


```plaintext
Correo:    admin@example.com
Contraseña: changeme
```

> Cámbialas al ingresar por primera vez.

---

## 💡 Recomendaciones

* Cambia las credenciales por defecto apenas ingreses.
* Asocia dominios reales con registros A o CNAME para usar SSL.
* Usa esta herramienta solo en entornos seguros o con firewall.


