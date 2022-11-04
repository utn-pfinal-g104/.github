# PictogAR

Por ahora en el server linux esta todo abierto:  

API:       http://20.115.17.201:5080/                   =>   pictog.ar:5080  
WEBAPP:    http://20.115.17.201 (puerto 80 default)     =>   pictog.ar  
DB         20.115.17.201,1334                           =>   pictog.ar,1334  
STORAGE    http://20.115.17.201:10000/                  =>   pictog.ar:10000  
 

Cualqueir **commit a los branch principales** de la API o la WEB, buildea una imagen de docker, la pushea al ghcr.io y despues **Deployea** por SSH en el server.  

Las passwords estan expuestas en el appsettings.production de la api.  

Para levantar todo el entorno localmente tienen que ejecutar el *docker-compose.yml* que esta en el repo de la API:  
``` docker-compose up ```  
Para que funcione tienen que primero estar logeados al container registry, se loguean con su usuario de github y un access token de github.  
Una vez que tienen ese token ejecutan: ``` docker login ghcr.io -u {Github Username} -p {TOKEN} ```  
Y listo despues de esto ya pueden pullear las imagenes del registry  


## LOGS

Primero hay que conectarse por SSH al servidor:
``` bash
ssh 20.115.17.201 -l pictogar-user
```
password: qweQWE123!@#

Una vez dentro del server corremos el siguiente comando
``` bash
sudo docker-compose --file ~/pictogar/docker-compose.yml logs -f -t pictogar-api
``` 
pictogar-api puede ser reemplazado por pictogar-web, pictogar-database o pictogar-storage.
Tambien se puede dejar vacio y se veran los logs de todo en simultaneo.

Para dejar de escuchar los logs tocan CTRL + C y para salir del SSH del server escriben 
``` bash
exit
```
en la consola.

## Para reiniciar todos los deploys del server y arrancar con todo en cero
Entran por ssh como para los logs, y una vez ahi corren:
``` bash
sudo docker-compose --file ~/pictogar/docker-compose.yml down && sudo docker-compose --file ~/pictogar/docker-compose.yml up 
```

### Importante:  
El server solo esta prendido entre las 11AM y las 11PM, fuera de ese rango esta apagado pero lo pueden startear a mano desde el Azure Portal

### Inicializacion:
Ejecutar el endpoint /pictogramas/guardar para descargar de arasaac todos los pictogramas en la db y el storage (Solo una vez)
