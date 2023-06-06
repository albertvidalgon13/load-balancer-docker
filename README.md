------
EJECUCIÓN:
    1. Descargar los 4 ficheros: docker-compose.yml, nginx.conf, certificate.crt y private_key.key (he añadido el fichero certificate.csr adicionalmente).
    2. Desde el directorio donde estan todos los archivos, ejecutar:
        $ docker-compose up
        $ docker-compose up -d (en caso de no querer ver los logs)
    3. Una vez hecho esto, ya simplemente tendremos que entrar en el navegador y acceder a la url para ver el servicio
        https://localhost:8080 (desde dentro de la máquina)
        https://IP_HOST:8080 (desde fuera de la máquina)
------
IMPLEMENTACIÓN:

docker-compose.yml:
    Docker compose simple de un load balancer donde he definido también una network en modo bridge. Defino dos contenedores con la imagen de hello-kubernetes:1.10 las cuales harán el load balancer. También añado los puertos 8080 para acceder al servicio (aunque podrían ser otros).

nginx.conf
    Archivo de configuración del nginx que he usado para hacer el load balancer. Definimos el upstream con las dos imagenes que hemos creado en el docker compose. En el apartado de server definimos los certificados que tiene que usar para poder hacer el https y la url. 
    No he definido ninguna regla para http asi que no deja acceder al servicio mediante http://localhost:8080. Tambien esta configurado en default la distribucion de los hosts por lo que se usa round-robin (por orden, una cada vez).

certificados:
    He usado la herramienta OpenSSL
------
