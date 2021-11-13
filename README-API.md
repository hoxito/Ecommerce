<a name="top"></a>
# StatsGo Service v0.1.0

Microservicio de Estadisticas

- [RabbitMQ_POST](#rabbitmq_post)
	- [Invalidar Token](#invalidar-token)
	
- [Estadisticas](#Estadisticas)
	- [Listar Ordenes](#Ordenes)
	- [Listar Usuarios](#Usuarios)
	- [Listar Productos](#Productos)
   
	


# <a name='rabbitmq_post'></a> RabbitMQ_POST

## <a name='invalidar-token'></a> Invalidar Token
[Back to top](#top)

<p>AuthService enviá un broadcast a todos los usuarios cuando un token ha sido invalidado. Los clientes deben eliminar de sus caches las sesiones invalidadas.</p>

	FANOUT auth/fanout





### Success Response

Mensaje

```
{
   "type": "logout",
   "message": "{Token revocado}"
}
```


# <a name='Estadisticas'></a> Estadisticas

## <a name='Ordenes'></a> Listar Ordenes
[Back to top](#top)

<p>Devuelve una lista segun los parametros de busqueda.</p>

	GET /v1/stats/{Query}



### Examples

{url}/v1/stats/?select=[estado,montomin,montomax,fechadesde,fechahasta]&orderby=fechadesde&items=1&pag=1

Header Autorización

```
Authorization=bearer {token}
```


### Success Response

Respuesta

```
HTTP/1.1 200 OK
  [{
       "id": "{Id Orden}",
       "estado": "{Estado de la orden}",
       "montomin": "{monto minimo total de la orden}",
       "montomax: "{monto maximo total de la orden}",
       "fechadesde": {fecha de creacion de la orden}
       "fechahasta": {fecha de finalizacion de la orden}

    }, ...]
```


### Error Response

401 Unauthorized

```
HTTP/1.1 401 Unauthorized
{
   "error" : "Unauthorized"
}
```
400 Bad Request

```
HTTP/1.1 400 Bad Request
{
   "messages" : [
     {
       "path" : "{Nombre de la propiedad}",
       "message" : "{Motivo del error}"
     },
     ...
  ]
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server Error
{
   "error" : "Not Found"
}
```

## <a name='Usuarios'></a> Deshabilitar Usuario
[Back to top](#top)

<p>Deshabilita un usuario en el sistema.   El usuario logueado debe tener permisos &quot;admin&quot;.</p>

	POST /v1/users/:userId/disable



### Examples

Header Autorización

```
Authorization=bearer {token}
```


### Success Response

Respuesta

```
HTTP/1.1 200 OK
```


### Error Response

401 Unauthorized

```
HTTP/1.1 401 Unauthorized
{
   "error" : "Unauthorized"
}
```
400 Bad Request

```
HTTP/1.1 400 Bad Request
{
   "messages" : [
     {
       "path" : "{Nombre de la propiedad}",
       "message" : "{Motivo del error}"
     },
     ...
  ]
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server ErrorListar 
{Listar 
   "error" : "Not Found"Listar 
}
```
## <a name='Productos'></a> Listar Productos
[Back to top](#top)

<p>Habilita un usuario en el sistema. El usuario logueado debe tener permisos &quot;admin&quot;.</p>

	POST /v1/users/:userId/enable



### Examples

Header Autorización

```
Authorization=bearer {token}
```


### Success Response

Respuesta

```
HTTP/1.1 200 OK
```


### Error Response

401 Unauthorized

```
HTTP/1.1 401 Unauthorized
{
   "error" : "Unauthorized"
}
```
400 Bad Request

```
HTTP/1.1 400 Bad Request
{
   "messages" : [
     {
       "path" : "{Nombre de la propiedad}",
       "message" : "{Motivo del error}"
     },
     ...
  ]
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server Error
{
   "error" : "Not Found"
}
```
## <a name='usuarios'></a> Listar Usuarios
[Back to top](#top)

<p>Obtiene información de todos los usuarios.</p>

	GET /v1/users



### Examples

Header Autorización

```
Authorization=bearer {token}
```


### Success Response

Respuesta

```
    HTTP/1.1 200 OK
    [{
       "id": "{Id usuario}",
       "name": "{Nombre del usuario}",
       "login": "{Login de usuario}",
       "permissions": [
           "{Permission}"
       ],
	      "enabled": true|false
    }, ...]
```


### Error Response

401 Unauthorized

```
HTTP/1.1 401 Unauthorized
{
   "error" : "Unauthorized"
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server Error
{
   "error" : "Not Found"
}
```
## <a name='login'></a> Login
[Back to top](#top)

<p>Loguea un usuario en el sistema.</p>

	POST /v1/user/signin



### Examples

Body

```
{
  "login": "{Login de usuario}",
  "password": "{Contraseña}"
}
```


### Success Response

Respuesta

```
HTTP/1.1 200 OK
{
  "token": "{Token de autorización}"
}
```


### Error Response

400 Bad Request

```
HTTP/1.1 400 Bad Request
{
   "messages" : [
     {
       "path" : "{Nombre de la propiedad}",
       "message" : "{Motivo del error}"
     },
     ...
  ]
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server Error
{
   "error" : "Not Found"
}
```
## <a name='logout'></a> Logout
[Back to top](#top)

<p>Desloguea un usuario en el sistema, invalida el token.</p>

	GET /v1/user/signout



### Examples

Header Autorización

```
Authorization=bearer {token}
```


### Success Response

Respuesta

```
HTTP/1.1 200 OK
```


### Error Response

401 Unauthorized

```
HTTP/1.1 401 Unauthorized
{
   "error" : "Unauthorized"
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server Error
{
   "error" : "Not Found"
}
```
## <a name='otorga-permisos'></a> Otorga Permisos
[Back to top](#top)

<p>Otorga permisos al usuario indicado, el usuario logueado tiene que tener permiso &quot;admin&quot;.</p>

	POST /v1/users/:userId/grant



### Examples

Body

```
{
  "permissions" : ["permiso", ...],
}
```
Header Autorización

```
Authorization=bearer {token}
```


### Success Response

Respuesta

```
HTTP/1.1 200 OK
```


### Error Response

401 Unauthorized

```
HTTP/1.1 401 Unauthorized
{
   "error" : "Unauthorized"
}
```
400 Bad Request

```
HTTP/1.1 400 Bad Request
{
   "messages" : [
     {
       "path" : "{Nombre de la propiedad}",
       "message" : "{Motivo del error}"
     },
     ...
  ]
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server Error
{
   "error" : "Not Found"
}
```
## <a name='registrar-usuario'></a> Registrar Usuario
[Back to top](#top)

<p>Registra un nuevo usuario en el sistema.</p>

	POST /v1/user



### Examples

Body

```
{
  "name": "{Nombre de Usuario}",
  "login": "{Login de usuario}",
  "password": "{Contraseña}"
}
```


### Success Response

Respuesta

```
HTTP/1.1 200 OK
{
  "token": "{Token de autorización}"
}
```


### Error Response

400 Bad Request

```
HTTP/1.1 400 Bad Request
{
   "messages" : [
     {
       "path" : "{Nombre de la propiedad}",
       "message" : "{Motivo del error}"
     },
     ...
  ]
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server Error
{
   "error" : "Not Found"
}
```
## <a name='revoca-permisos'></a> Revoca Permisos
[Back to top](#top)

<p>Quita permisos al usuario indicado, el usuario logueado tiene que tener permiso &quot;admin&quot;.</p>

	POST /v1/users/:userId/revoke



### Examples

Body

```
{
  "permissions" : ["permiso", ...],
}
```
Header Autorización

```
Authorization=bearer {token}
```


### Success Response

Respuesta

```
HTTP/1.1 200 OK
```


### Error Response

401 Unauthorized

```
HTTP/1.1 401 Unauthorized
{
   "error" : "Unauthorized"
}
```
400 Bad Request

```
HTTP/1.1 400 Bad Request
{
   "messages" : [
     {
       "path" : "{Nombre de la propiedad}",
       "message" : "{Motivo del error}"
     },
     ...
  ]
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server Error
{
   "error" : "Not Found"
}
```
## <a name='usuario-actual'></a> Usuario Actual
[Back to top](#top)

<p>Obtiene información del usuario actual.</p>

	GET /v1/users/current



### Examples

Header Autorización

```
Authorization=bearer {token}
```


### Success Response

Respuesta

```
HTTP/1.1 200 OK
{
   "id": "{Id usuario}",
   "name": "{Nombre del usuario}",
   "login": "{Login de usuario}",
   "permissions": [
       "{Permission}"
   ]
}
```


### Error Response

401 Unauthorized

```
HTTP/1.1 401 Unauthorized
{
   "error" : "Unauthorized"
}
```
500 Server Error

```
HTTP/1.1 500 Internal Server Error
{
   "error" : "Not Found"
}
```
