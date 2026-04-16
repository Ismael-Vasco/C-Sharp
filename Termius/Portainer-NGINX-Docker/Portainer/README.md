# 🐳 Portainer con Docker Compose

### URL de referencia
[YouTube: Cómo instalar Portainer con Docker Compose](https://www.youtube.com/watch?v=ytpYVClppzg)

Este proyecto despliega una instancia de **Portainer CE** (Community Edition) utilizando `docker-compose`. Portainer es una interfaz gráfica que facilita la gestión de contenedores Docker, volúmenes, redes y stacks.

---

## 📋 Descripción

Portainer es una herramienta de gestión de contenedores Docker que proporciona una interfaz web intuitiva para administrar contenedores, imágenes, volúmenes, redes y stacks. Es especialmente útil para entornos de desarrollo y producción donde se necesita una gestión visual de Docker.

### Características principales
- Interfaz web fácil de usar
- Gestión de contenedores, imágenes y volúmenes
- Creación y gestión de stacks con Docker Compose
- Autenticación de usuarios y equipos
- Registros de contenedores en tiempo real
- API REST para integración

---

## 📦 Requisitos

- **Docker**: Versión 20.10 o superior
- **Docker Compose**: Versión 2.0 o superior
- **Sistema operativo**: Linux, macOS o Windows con Docker Desktop

---

## 🔧 Requisitos previos

Antes de ejecutar Portainer, asegúrate de crear la red y el volumen externos utilizados en el `docker-compose.yml`:

### Crear la red externa
```bash
docker network create general-net
```

### Crear el volumen externo
```bash
docker volume create portainer_data
```

Estos recursos son compartidos con otros servicios en el proyecto (como NGINX).

---

## 🚀 Instalación y ejecución

1. **Clona o navega al directorio del proyecto**:
   ```bash
   cd Termius/Portainer-NGINX-Docker/Portainer
   ```

2. **Ejecuta Portainer**:
   ```bash
   docker-compose up -d
   ```

   El flag `-d` ejecuta los contenedores en segundo plano.

3. **Verifica que esté corriendo**:
   ```bash
   docker-compose ps
   ```

---

## ⚙️ Configuración inicial

1. **Accede a la interfaz web**:
   - Abre tu navegador y ve a: `http://localhost:9000` (o `http://tuhost:9000` si estás en un servidor remoto)

2. **Primer inicio de sesión**:
   - Crea una cuenta de administrador con un nombre de usuario y contraseña seguros.
   - Selecciona "Local" como entorno Docker (ya que estamos usando el socket de Docker del host).

3. **Configuración adicional** (opcional):
   - Configura autenticación externa (LDAP, OAuth)
   - Crea equipos y usuarios adicionales
   - Configura notificaciones

---

## 🔌 Puertos y acceso

- **9000**: Interfaz web de Portainer
- **8000**: Puerto para conexiones de agentes (usado para entornos remotos)

Asegúrate de que estos puertos estén disponibles y no bloqueados por firewalls.

---

## 📁 Estructura del proyecto

```
Portainer/
├── docker-compose.yml    # Configuración de Docker Compose
└── README.md            # Este archivo
```

### Archivo docker-compose.yml

El archivo `docker-compose.yml` incluye:
- **Imagen**: `portainer/portainer-ce:latest` (última versión de Community Edition)
- **Puertos**: 8000 y 9000 mapeados al host
- **Volúmenes**:
  - `/var/run/docker.sock`: Permite a Portainer gestionar Docker
  - `portainer_data`: Almacena configuración y datos persistentes
- **Red**: `general-net` (externa, compartida con otros servicios)
- **Reinicio**: `always` (reinicia automáticamente en caso de fallo)

---

## 🛠️ Uso básico

### Gestionar contenedores
1. Inicia sesión en Portainer
2. Ve a "Containers" en el menú lateral
3. Puedes ver, iniciar, detener, eliminar contenedores
4. Haz clic en un contenedor para ver logs, estadísticas, etc.

### Gestionar imágenes
- Ve a "Images" para ver y gestionar imágenes Docker

### Crear stacks
1. Ve a "Stacks"
2. Crea un nuevo stack con un archivo docker-compose.yml
3. Portainer desplegará los servicios automáticamente

### Gestionar volúmenes y redes
- Usa las secciones "Volumes" y "Networks" para gestión avanzada

---

## 🔒 Seguridad

- **Cambia la contraseña por defecto**: Usa una contraseña fuerte para la cuenta de administrador
- **Acceso restringido**: Limita el acceso a la interfaz web solo a redes confiables
- **Actualizaciones**: Mantén Portainer actualizado para parches de seguridad
- **Socket de Docker**: El montaje de `/var/run/docker.sock` da acceso completo a Docker; úsalo con precaución

---

## 🐛 Solución de problemas

### No puedo acceder a la interfaz web
- Verifica que el contenedor esté corriendo: `docker-compose ps`
- Revisa los logs: `docker-compose logs portainer`
- Asegúrate de que el puerto 9000 no esté ocupado

### Error de conexión con Docker
- Verifica que Docker esté corriendo en el host
- Comprueba permisos del socket: `ls -la /var/run/docker.sock`

### Problemas con la red externa
- Asegúrate de que la red `general-net` existe: `docker network ls`
- Si no existe, créala: `docker network create general-net`

---

## 🛑 Detener y limpiar

Para detener Portainer:
```bash
docker-compose down
```

Para detener y eliminar volúmenes (¡cuidado, borra datos!):
```bash
docker-compose down -v
```

---

## 📚 Recursos adicionales

- [Documentación oficial de Portainer](https://docs.portainer.io/)
- [GitHub de Portainer](https://github.com/portainer/portainer)
- [Docker Compose documentation](https://docs.docker.com/compose/)

---

## 🤝 Contribución

Si encuentras errores o mejoras, por favor abre un issue o envía un pull request.

---

*Última actualización: Abril 2024*


