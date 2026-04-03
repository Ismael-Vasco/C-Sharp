## Container installation - Database -

**``The following commands are used to install docker, MySQL & PostgreSQL containers``**

### MySQL
```ps
docker run --name <NAME> -p<EXTERNAL PORT>:<INTERNAL PORT> -e MYSQL_ROOT_PASSWORD=<YOUR PASSWORD> -d mysql
```

### PostgreSQL
```ps
docker run --name <NAME> -p<EXTERNAL PORT>:<INTERNAL PORT> -e POSTGRES_PASSWORD=<YOUR PASSWORD> -d postgres
```

### IMPORTANT
#### run
This means that the container must be completely ``create`` and ``start``.
#### --name
This assigns an specific ``name`` to the container.
#### -p
This means the **Publish Ports** ``-p<EXTERNAL PORT>:<INTERNAL PORT>``
- **EXTERNAL PORT** -> It is the HOST (users) port
- **INTERNAL PORT** -> It is the LOCAL (container) port

#### -e
This means ``ENVIRONMENT VARIABLES``
#### -d ``--DETACH``
This means the container runs in the ``background``.
