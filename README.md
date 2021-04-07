
# oauth-v2-api

  
  

## Client Credentials

> El modelo más sencillo de autenticarse de OAuth 2.0 es Client Credentials. Se usa para la autenticación de máquina a máquina, donde no se requiere el permiso de un usuario específico para acceder a los datos.

>

>Su funcionamiento consiste en realizar una petición al servidor en el endpoint del generador de tokens:

  
### EndPoint
```
POST /v1/api/oauth-v2/token
```

### Cabeceras de la petición:
```
Host: authorization-server.com

Accept: application/json

Content-Type: application/json

Content-Length: ...
```

  

### Donde

- **scope:** podría ser cualquier valor que ayude a autorizar el uso de nuestras aplicaciones.
- **realm:** Identificador especifico del negocio, el cual se otorga por el administrador del sistema. 
- **client_id:** Es el identificador público de la aplicación. Una aplicación es el resultado de registrar un nuevo cliente en nuestro servidor OAuth.
- **client_secret:** Es una contraseña o llave secreta que generaremos en el servidor de OAuth en relación con el cliente (la aplicación).

### Body
> Deberá estar presente en el cuerpo de la petición en formato Json los siguientes parámetros:

```
{
	"grant_type":"client_credentials",
	"scope":"Descripcion de la solicitud del token"
}

``` 


> La respuesta directamente será el Access Token:


```

HTTP/1.1 200 OK

Cache-Control: no-store

Pragma: no-cache

Content-Type: application/json

Content-Length: ...
  

{
  "status": 201,
  "body": {
    "token_id": "4febfe80-970c-11eb-baee-63261ef7f48b",
    "chanel_id": "3af1acc0-02c2-11eb-8967-1baaf9b822a3",
    "type_token_id": "5aca2e90-02c3-11eb-83d1-519c63ca7eb5",
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyZWFsbSI6IjNhZjFhY2MxLTAyYzItMTFlYi04OTY3LTFiYWFmOWI4MjJhMyIsImNsaWVudF9pZCI6IjNhZjFhY2MwLTAyYzItMTFlYi04OTY3LTFiYWFmOWI4MjJhMyIsImNsaWVudF9zZWNyZXQiOiI0MTU0NGVjMS0wMmMxLTExZWItOWVhMy1lOTVjYTA5NGJiY2IiLCJpYXQiOjE2MTc3MzY0NzB9.4VbrYXVAIuw06XFj_bnhu75sfJRdWgRuyBsGmGAOkJk",
    "date_expiration": "2021-04-06T20:16:42.759Z",
    "refresh_token": "50046880-970c-11eb-baee-63261ef7f48b",
    "scope": "50046881-970c-11eb-baee-63261ef7f48b",
    "user_agent": "insomnia/2021.2.2",
    "state": "",
    "date_created": "2021-04-06T19:14:30.526Z",
    "ip": null,
    "active": true
  }
}

```  

### Access Token

> La respuesta de todos los métodos de autenticación al final tiene que ser un formato semejante: un JSON con los siguientes valores:
  

- access_token (requerido) Suele ser un JWT que después usaremos para autenticar las peticiones a una API.

- token_type (requerido) El tipo de token que vamos a usar. Generalmente, al usar JWT, se usa el valor “Bearer”.

- expires_in (recomendado) Indica la duración en segundos del access_token. Una vez caduca puede ser renovado usando el Grant Type de Refresh Token.

- refresh_token (opcional) Si el access_token va a expirar y nos permiten volver a generar el token, necesitaremos este valor en el proceso de Refresh Token.

- scope (opcional) Es un parámetro que se utiliza para autorizar un token en un contexto concreto. Generalmente, nuestra API buscará un scope concreto para el que se ha autorizado el token que le envían.

- id_token (opcional) Si se utiliza un scope con valor “openid”, puede significar que queremos utilizar OpenId Connect (OIDC) para autenticarnos. En ese supuesto, puede aparecer un JWT extra donde encontraremos la información sobre el perfil del usuario.


# Consumo API TVE

> El API con la cual se calculan los dato de  **tromboprofilaxis** efectiva esta orientada a la recepción de data con la cual un motor de inferencia como sistema experto esta en capacidad de determinar la efectividad de la aplicación de los protocolos encaminados a prevenir la **tromboprofilaxis**
## EndPoint 
> Para tal fin se destina como acceso al api la el siguiente path : 

```
	POST /administrator/api/v1/tve-masive
```

### Cabeceras de la petición:
```
Host: authorization-server.com

Accept: application/json

Content-Type: application/json

realm: 3af1acc1-02c2-11eb-8967-1baaf9df22a3

client_id: 3af1acc0-02c2-11eb-8967-1bacb9b822a3

client_secret: 41544ec1-02c1-11eb-9ea3-e95ca094cbcb

authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyZWFsbSI6IjNhZjFhY2MxLTAyYzItMTFlYi04OTY3LTFiYWFmOWI4MjJhMyIsImNsaWVudF9pZCI6IjNhZjFhY2MwLTAyYzItMTFlYi04OTY3LTFiYWFmOWI4MjJhMyIsImNsaWVudF9zZWNyZXQiOiI0MTU0NGVjMS0wMmMxLTExZWItOWVhMy1lOTVjYTA5NGJiY2IiLCJpYXQiOjE2MTQyMzQyOTN9.6BuNFDwCk2pQNNTSgYxooEQWy61XUqVDqFjpDwnuV3k

Content-Length: ...
```

#### Donde: 
>
|**Cabecera**| **Descripción**  | **Tipo**  |
|--|--|--|
| **Content-Type** | Dice al cliente que tipo de contenido será retornado  | Opcional, valor por defecto "application/json"  |
|**Accept**|Anuncia que tipo de contenido el cliente puede procesar| Opcional, valor por defecto "application/json"|
|**realm**| Identificador especifico del negocio, el cual se otorga por el administrador del sistema|Obligatorio|
|**client_id**|Es el identificador público de la aplicación. Una aplicación es el resultado de registrar un nuevo cliente en nuestro servidor OAuth.|Obligatorio|
|**client_secret** |Es una contraseña o llave secreta que generaremos en el servidor de OAuth en relación con el cliente (la aplicación).|Obligatorio|
|**authorization**|contiene las credenciales para autenticar a un usuario en un servidor, para nuestro caso el servidor de autorizaciones de **oauth-v2-api** Deberá contener el prefijo **Bearer** Token |Obligatorio|

### Body
> Deberá estar presente en el cuerpo de la petición en formato Json de tipo Array bajo la siguiente definición como objeto que tiene estos atributos con sus tipos:

```json
[{
		etv: string;

		escala: Object;

		service: Object;

		description: string;

		covid: string;

		sexo: string;

		factores: string;

		fac_nacimiento: date;

		peso: number;

		estatura: number;

		edad: number;

		rango_edad: string;

		imc: number;

		procedimiento: string;

		creatinina: string;

		value: number;

		tgf: number;

		fecha_cx: date;

		fecha_egreso: date;

		tipoFactor: string;

		improve: string;

		chest: string;

		riesgo_sangrado: string;

		fecha_inicio_trombo: string;

		tipo_tto_hx: string;

		molecula: string;

		egreso_farmacologico: string;

		contraindicaciones: string;
}]
``` 

| **Propiedad** | **Tipo**  | **Posibles valores** | **Observaciones** |
|--|--|--|--|
| etv | string | "Si" o "No" | Responde a la pregunta:  | |
|escala |Object | Objeto que responde a la entidad de escala | Consumir servicio tipo Get del api  [/administrator/api/v1/poll](#)|
|service |Object | Objeto que responde a la entidad de service| Consumir servicio tipo Get del api  [administrator/api/v1/services](#)|
| description| string | "Cualquier observación" | Responde a la pregunta:  |
| covid| string | "Si", "No", "No Reporta" | Responde a la pregunta: ¿Tienen covid? | 
| sexo| string | "Hombre", "Mujer" | Responde a la pregunta: ¿Sexo? | 
| fac_nacimiento| date| "27/10/1988" | Responde a la pregunta: ¿Fecha de nacimiento? | 
| peso| number| 70 | Responde a la pregunta: ¿peso del paciente? debe estar entre un rango de 0 a 300 kg | 
| estatura| number| 1.50 | Responde a la pregunta: ¿Estatura del paciente? debe ser un numero entero con maximo tres decimales y no debe ser superior a 3 | 
| edad| number| 25 | Responde a la pregunta: ¿Edad del paciente? debe ser un numero entero no mayor a 150 | 
| rango_edad| string| "Menor a 40 Años" o "40 a 59 Años" o "60 a 74 Años" o "75 años o mayor" | | 
| imc| number| 25.26 | Numerico que responde al calculo del indice de masa corporal y soporta hasta dos decimales | 
| creatinina| string| "SI" o "NO" | Responde a la pregunta: ¿Tiene creatinina el paciente? | 
| value| number| 32 | Responde al valor de la creatinina |
| tgf| number| 32 | Responde al valor de la tasa de filtración glomerular |
| fecha_cx| date| "27/10/1988" | Responde a la pregunta: ¿Fecha de nacimiento? | 
| fecha_egreso| date| "27/10/1988" | Responde a la pregunta: ¿Fecha de nacimiento? | 






# Errores Conocidos:
### Sin autenticación:
```json
{
  "status": 412,
  "body": [
    {
      "status": 412,
      "error": "La propiedad authorization no esta presente en la petición"
    },
    {
      "status": 412,
      "error": "La propiedad realm no esta presente en la petición"
    },
    {
      "status": 412,
      "error": "La propiedad client_id no esta presente en la petición"
    },
    {
      "status": 412,
      "error": "La propiedad client_secret no esta presente en la petición"
    }
  ]
}
``` 



