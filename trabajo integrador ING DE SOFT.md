  
Una cámara de video control vial, mide la velocidad con la que los autos pasan por una calle. En la ciudad, se cuentan con *n* cantidad de cámaras. Cada cámara detecta automáticamente al vehículo cuando pasa y envía a nuestro sistema los siguientes datos: fecha y hora, id de la cámara, patente y velocidad. El paso de cada vehículo deberá registrarse en el sistema. Cada cámara tiene un id, una descripción, coordenadas x e y de su ubicación, dirección IP y modelo de la cámara. El sistema debe funcionar 24/7.

Cuando el sistema recibe los datos de un vehículo que pasó, el sistema realiza distintas acciones según la velocidad: //no es requerimiento pero sí reglas 

* si la velocidad es mayor a 70km/h:  
  * el sistema envía los datos a una API que se encargará de guardarlos en una base de datos  
  * el sistema envía un correo con los datos que envió la cámara a la cuenta "avisos@ciudad"  
* si la velocidad es mayor a 100km/h:  
  * el sistema envía los datos a una API que se encargará de guardarlos en una base de datos  
  * el sistema envía un correo con los datos que envió la cámara a la cuenta "alertas@ciudad"  
  * el sistema envía, 3 veces, los datos recibidos por la cámara a una impresora para que sean impresos  
    

REQUERIMIENTOS:

* Funcional:   
- Debe detectar los vehículos que pasan  
- Debe enviar los datos al sistema   
- Debe registrar el paso de los vehículos en el sistema 

* No funcional:  
- Cada cámara contará con un Id, una descripción, ubicación, dirección IP y modelo de la cámara  
- El sistema funcionará las 24 hs del dia, todos los días   
    
* Dominio:   
- el sistema tendra que contar con una camara de velocidad

DICCIONARIO DE DATOS

veloc70= velocidad \+ datos \+ correo

| nombre | descripción  | longitud  | tipo  | dominio |
| :---- | :---- | :---- | :---- | :---- |
| velocidad | km en la que el vehículo pasó  | 3 digitos, 2 decimales  | float  | continuo |
| datos  | datos del vehículo por ejemplo patente, fecha y hora, etc  | string  100 char 20 int | char  | continuo  |
| correo  | correo donde se envia la informacion de los vehículos que excedieron la velocidad  | 14 char  | char  | dom |

veloc100=velocidad+api+correo+impreso

| nombre | descripción  | longitud  | tipo  | dominio |
| :---- | :---- | :---- | :---- | :---- |
| velocidad | velocidad en la que el vehículo pasó  | 3 digitos, 2 decimales  | float  | continuo |
| datos  | datos del vehículo por ejemplo patente, fecha y hora, etc  | string  100 char, 20 int o boleano | char  | continuo  |
| correo  | correo donde se envia la informacion de los vehículos que excedieron la velocidad  | 14 char  | char  | dom |
| impreso | impresion sobre los datos que el vehiculo sobrepaso la velocidad permitida | 100 string | char | continuo |

vehículo=  fecha \+ hora \+ idcam \+ patente \+ velocidad

| nombre | descripción | longitud | tipo | dominio  |
| ----- | ----- | ----- | ----- | ----- |
| fecha  | dia en el que el vehículo pasó  | 8 dígitos | date | continuo |
| hora  | hora en la que el vehículo pasó  | 6 dígitos  | time | continuo |
| patente  | identificacion del vehiculo  | 3 digitigos 4 char | string | discreto |
| velocidad  | velocidad en la que el vehículo circulaba  | 3 dígitos 2 decimales | float | discreto |

camara= id \+ desc \+ ubicación \+ direcIP \+ modcam

| nombre  | descripción  | longitud | tipo  | dominio |
| :---- | :---- | :---- | :---- | :---- |
| id | número de identificación de cada cámara  | 5 dígitos | int | continuo |
| desc | descripción de la camara | 50 char  | string | continuo  |
| ubicación | lugar donde se encuentra colocada la cámara | 100 char | string | continuo |
| direcIP | dirección ip única de cada cámara  |  12 int | int | continuo |
| modcam | modelo de la cámara | 5 digitos | int | continuo |

REGLAS DE NEGOCIO 

* Hechos:  
- las cámaras van a medir la velocidad en la que pasan los vehículos  
- el paso de cada vehículo va a quedar registrado en el sistema


* Acciones disparadoras:   
- si la velocidad es mayor a 70 km, el sistema envía los datos a una api que se encarga de guardarlos que se encarga de guardarlos en una base de datos


- si la velocidad es mayor a 100 km, el sistema envía los datos a una api que se encarga de guardarlos en una base de datos 


- Cuando el sistema recibe los datos de un vehículo que pasó, el sistema realiza distintas acciones según la velocidad 

* Inferencias:   
- En caso de que pase un vehículo, el sistema realizará distintas acciones dependiendo la velocidad. si la velocidad es mas de 70km o mas de 100km 

CASO DE USO 

caso de uso: control y registro de velocidades

actores: camara (primario)

caminos básicos:

1. la cámara envía los datos al sistema   
2. el sistema va a registrar los datos y luego va evalúa los datos de velocidad

camino alternativos:   
2.a el sistema detecta que el vehículo circula dentro de la velocidad permitida, hasta 70 km. fin de caso de uso

2.b el sistema detecta que el vehículo va mayor a 70 km y menos que 100 km  
2.b.1 el sistema los envía a una API. El sistema envía un correo con los datos que envió la cámara al mail “alertas@ciudad”. fin de caso de uso

2.c el sistema detecta que el vehículo va mayor a 100 km   
2.c.1 el sistema lo envía a una API. El sistema envía un correo con los datos que envió la cámara al mail “alertas@ciudad”. Por último  envía 3 veces, los datos recibidos por la cámara a la impresora, para que sean impresos. fin de caso de uso 

escenario de éxito: 

2.a el sistema detecta que el vehículo va a menos de 70 km

2.b el sistema detecta que excede la velocidad a mas de 70km y logró enviar los datos al mail “alertas@ciudad”

2.c el sistema detecta que excede la velocidad a más de 100km y logró enviar los datos al mail “alertas@ciudad”. luego envió los datos a la impresora para que sean impresos   
