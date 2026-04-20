# CASO: `sha256_password` is deprecated

## PASO 1 — Entra a MySQL
```docker
docker exec -it nombre_mysql mysql -uroot -p
```
- Ingresar su MySQL password

## PASO 2 — Ver qué usuarios usan ese plugin
```sql
SELECT user, host, plugin FROM mysql.user;
```

## PASO 3 — Cambiar el plugin
### Para cada usuario:
```sql
ALTER USER 'root'@'%' IDENTIFIED WITH caching_sha2_password BY 'tu_password';
```

## PASO 4 — Aplicar cambios
```sql
FLUSH PRIVILEGES;
```

## PASO 5 — Reiniciar contenedor
```docker
docker restart nombre_mysql
```
