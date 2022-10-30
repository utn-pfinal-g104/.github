# PictogAR

Por ahora en el server linux esta todo abierto:  

API:       http://20.115.17.201:5000/  
WEBAPP:    http://20.115.17.201:3000/  
DB         20.115.17.201,1334    
STORAGE    http://20.115.17.201:10000/  


Cualqueir **commit a los branch principales** de la API o la WEB, buildea una imagen de docker, la pushea al ghcr.io y despues **Deployea** por SSH en el server.  

Las passwords estan expuestas en el appsettings.production de la api.  

Para levantar todo el entorno localmente tienen que ejecutar el *docker-compose.yml* que esta en el repo de la API:  
``` docker-compose up ```  
Para que funcione tienen que primero estar logeados al container registry, se loguean con su usuario de github y un access token de github.  
Una vez que tienen ese token ejecutan: ``` docker login ghcr.io -u {Github Username} -p {TOKEN} ```  
Y listo despues de esto ya pueden pullear las imagenes del registry  



### Importante:  
El server solo esta prendido entre las 11AM y las 11PM, fuera de ese rango esta apagado pero lo pueden startear a mano desde el Azure Portal
