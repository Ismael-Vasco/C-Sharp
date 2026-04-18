# Recuperar acceso sin perder datos (más seguro pero más pasos)
## Detén el contenedor:
```
docker stop some-mysql
```
## Arranca temporalmente en modo skip-grant-tables:
```
docker run --rm -it \
  --name mysql-recovery \
  --volumes-from some-mysql \
  mysql:latest \
  mysqld --skip-grant-tables --skip-networking
```
## En otra terminal, conéctate:
```
docker exec -it mysql-recovery mysql -u root
```
## Cambia el password:
```
FLUSH PRIVILEGES;
ALTER USER 'root'@'%' IDENTIFIED BY 'nuevopassword';
ALTER USER 'root'@'localhost' IDENTIFIED BY 'nuevopassword';
```
## Detén el contenedor recovery y vuelve a levantar el original:
```
docker stop mysql-recovery
docker start some-mysql
```
