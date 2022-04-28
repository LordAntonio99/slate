---
title: Pumpum API

language_tabs:
  - shell
  - python
  - javascript

toc_footers:

includes:
  - errors.md

search: true
code_clipboard: true
---

# Introducción

Bienvenido a la API de Pumpum! Puedes usar nuestra API para ver el funcionamiento de la página web, tanto en el manejo de usuarios como con la base de datos que contiene todo.

Esta documentación esta disponible con los lenguajes de Shell (curl), Python y Javascript! Para poder navegar y ver los ejemplos con los diferentes lenguajes, los encontrarás en forma de pestaña en la sección de arriba a la derecha de la página.

Esta web está creada única y exclusivamente para la realización de un proyecto de fin de grado.

# Autenticación

## Registro

> Para crear un nuevo usuario utilizar el siguiente código:

```python
import requests

url = "http://localhost:3000/api/auth/register"

payload = "{\r\n    \"email\": \"demo@pruebas.local\",\r\n    \"password\": \"123\",\r\n    \"username\": \"Demo\"\r\n}"
headers = {}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'http://localhost:3000/api/auth/register' \
--data-raw '{
    "email": "demo@pruebas.local",
    "password": "123",
    "username": "Demo"
}'
```

```javascript
var raw = "{\r\n    \"email\": \"demo@pruebas.local\",\r\n    \"password\": \"123\",\r\n    \"username\": \"Demo\"\r\n}";

var requestOptions = {
  method: 'POST',
  body: raw,
  redirect: 'follow'
};

fetch("http://localhost:3000/api/auth/register", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> Con una ejecución correcta, nos devolverá el siguiente objeto.

```json
{
    "username": "demo",
    "email": "demo@pruebas.local",
    "password": "U2FsdGVkX1+bJ6LHzzaFbct6CPr7LX5bTCrgrJURsrE=",
    "profilePic": "",
    "isAdmin": false,
    "_id": "6267e1da2d182b1e3465b1fe",
    "createdAt": "2022-04-26T12:13:14.096Z",
    "updatedAt": "2022-04-26T12:13:14.096Z",
    "__v": 0
}
```

Para poder realizar la mayoría de llamadas de la API, vamos a necesitar una nueva cuenta creada en la base de datos, ya que vamos a funcionar principalmente con el código "_id" único de cada usuario, y las sesiones con JWT.

Una vez nos hayamos registrado correctamente, deberemos dejar guardado nuestro "_id", para futuras llamadas a la api.

### HTTP Request

`POST http://localhost:3000/api/auth/register`

<aside class="notice">
Si la cuenta está creada, prueba con otros datos aleatorios. Sabrás que ha funcionado cuando la llamada devuelva el código 201.
</aside>

## Inicio de sesión

> Ejemplo de inicio de sesión

```python
import requests
 
url = "http://localhost:3000/api/auth/login"
 
payload = "{\r\n    \"email\": \"demo@pruebas.local\",\r\n    \"password\": \"123\"\r\n}"
headers = {}
 
response = requests.request("POST", url, headers=headers, data=payload)
 
print(response.text)
```

```shell
curl --location --request POST 'http://localhost:3000/api/auth/login' \
--data-raw '{
    "email": "demo@pruebas.local",
    "password": "123"
}'
```

```javascript
var raw = "{\r\n    \"email\": \"demo@pruebas.local\",\r\n    \"password\": \"123\"\r\n}";
 
var requestOptions = {
  method: 'POST',
  body: raw,
  redirect: 'follow'
};
 
fetch("http://localhost:3000/api/auth/login", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> Si el usuario es capaz de iniciar sesión, podremos observar que nos proporciona el código JWT:

```json
{
    "_id": "6267e1da2d182b1e3465b1fe",
    "username": "demo",
    "email": "demo@pruebas.local",
    "profilePic": "",
    "isAdmin": false,
    "createdAt": "2022-04-26T12:13:14.096Z",
    "updatedAt": "2022-04-26T12:13:14.096Z",
    "__v": 0,
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOmZhbHNlLCJpYXQiOjE2NTA5Nzc5NjcsImV4cCI6MTY1MTQwOTk2N30.45rizE5PZTxxLuIg8VAf9aqafwd0-H5rVcb6pDCV8A0"
}
```

Para la mayoría de las llamadas de la aplicación, vamos a necesitar del código JWT, el cual se nos da cuando iniciamos sesión, dentro del campo de <code>accessToken</code>.

Si nos ólvidamos de nuestro código o no lo hemos apuntado, podemos volver a efectuar esta llamada, ya que nos devolverá otra vez el mismo mientras sea válido por su duración.

### HTTP Request

`POST http://localhost:3000/api/auth/login`

<!-- <aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside> -->

# Usuarios

## Ver un usuario

> Ejecución para ver información de un usuario

```python
import requests
 
url = "http://localhost:3000/api/users/6267e1da2d182b1e3465b1fe"
 
payload={}
headers = {}
 
response = requests.request("GET", url, headers=headers, data=payload)
 
print(response.text)
```

```shell
curl --location --request GET 'http://localhost:3000/api/users/6267e1da2d182b1e3465b1fe'
```

```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};
 
fetch("http://localhost:3000/api/users/6267e1da2d182b1e3465b1fe", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> Nos devolverá el objeto del usuario seleccionado en la URL

```json
{
    "_id": "6267e1da2d182b1e3465b1fe",
    "username": "demo",
    "email": "demo@pruebas.local",
    "profilePic": "",
    "isAdmin": false,
    "createdAt": "2022-04-26T12:13:14.096Z",
    "updatedAt": "2022-04-26T12:13:14.096Z",
    "__v": 0
}
```

Mediante esta llamada a la API, podremos ver la información básica del usuario que hayamos elegido en la URL, no obstante, habrá algún dato, como la contraseña, que por seguridad no se mostrará, aunque esté encriptada.

Si no somos usuarios administradores, solo podremos ver nuestro usuario, no obstante, si lo somos, podremos ver la información de cualquier usuario.

### HTTP Request
`GET http://localhost:3000/api/users/<user id>`

## Ver todos los usuarios

```javascript
var myHeaders = new Headers();
myHeaders.append("Token", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MDk4MTU5NSwiZXhwIjoxNjUxNDEzNTk1fQ.Cm41J7_mgNitftVbilf5QGKTNLI9WTg1NXr3JZwt20I");
 
var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};
 
fetch("http://localhost:3000/api/users/", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python
import requests
 
url = "http://localhost:3000/api/users/"
 
payload={}
headers = {
  'Token': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MDk4MTU5NSwiZXhwIjoxNjUxNDEzNTk1fQ.Cm41J7_mgNitftVbilf5QGKTNLI9WTg1NXr3JZwt20I'
}
 
response = requests.request("GET", url, headers=headers, data=payload)
 
print(response.text)
```

```shell
curl --location --request GET 'http://localhost:3000/api/users/' \
--header 'Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MDk4MTU5NSwiZXhwIjoxNjUxNDEzNTk1fQ.Cm41J7_mgNitftVbilf5QGKTNLI9WTg1NXr3JZwt20I'
```

> La ejecución nos devolverá un array con todos los objetos de usuarios

```json
[
    {
        "_id": "6267e1da2d182b1e3465b1fe",
        "username": "demo",
        "email": "demo@pruebas.local",
        "password": "U2FsdGVkX1+bJ6LHzzaFbct6CPr7LX5bTCrgrJURsrE=",
        "profilePic": "",
        "isAdmin": true,
        "createdAt": "2022-04-26T12:13:14.096Z",
        "updatedAt": "2022-04-26T12:13:14.096Z",
        "__v": 0
    }
]
```

Esta llamada está reservada para los administradores únicamente.

El array que nos devolverá, contendrá los objetos de usuario de todos los usuarios con la misma estructura que lo tenía la anterior llamada.

Para la autenticación del usuario administrador, deberemos utilizar nuestro código JWT obtenido durante el inicio de sesión.

### HTTP Request

`GET http://localhost:3000/api/users/`

## Actualizar un usuario

> Ejemplo de llamada para actualizar un nombre de usuario

```shell
curl --location --request PUT 'http://localhost:3000/api/users/6267e1da2d182b1e3465b1fe' \
--header 'Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MDk4MTU5NSwiZXhwIjoxNjUxNDEzNTk1fQ.Cm41J7_mgNitftVbilf5QGKTNLI9WTg1NXr3JZwt20I' \
--header 'Content-Type: application/json' \
--data-raw '{
    "username": "demoActualizada"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Token", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MDk4MTU5NSwiZXhwIjoxNjUxNDEzNTk1fQ.Cm41J7_mgNitftVbilf5QGKTNLI9WTg1NXr3JZwt20I");
myHeaders.append("Content-Type", "application/json");
 
var raw = JSON.stringify({
  "username": "demoActualizada"
});
 
var requestOptions = {
  method: 'PUT',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};
 
fetch("http://localhost:3000/api/users/6267e1da2d182b1e3465b1fe", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python
import requests
import json
 
url = "http://localhost:3000/api/users/6267e1da2d182b1e3465b1fe"
 
payload = json.dumps({
  "username": "demoActualizada"
})
headers = {
  'Token': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MDk4MTU5NSwiZXhwIjoxNjUxNDEzNTk1fQ.Cm41J7_mgNitftVbilf5QGKTNLI9WTg1NXr3JZwt20I',
  'Content-Type': 'application/json'
}
 
response = requests.request("PUT", url, headers=headers, data=payload)
 
print(response.text)
```

> Nos devolverá el objeto con los nuevos datos del usuario

```json
{
    "_id": "6267e1da2d182b1e3465b1fe",
    "username": "demoActualizada",
    "email": "demo@pruebas.local",
    "password": "U2FsdGVkX1+bJ6LHzzaFbct6CPr7LX5bTCrgrJURsrE=",
    "profilePic": "",
    "isAdmin": true,
    "createdAt": "2022-04-26T12:13:14.096Z",
    "updatedAt": "2022-04-26T14:09:01.509Z",
    "__v": 0
}
```

Mediante esta llamada podemos editar cualquier tipo de campo que tenga el usuario dentro de la base de datos.

En el caso de modificar la contraseña, esta se encriptará de la misma forma que fue encriptada durante el registro.

Los usuarios administradores pueden editar cualquier usuario, pero los usuarios normales solo pueden modificar sus propios datos.

### HTTP Request
`PUT http://localhost:3000/api/users/<user id>`

## Borrar un usuario

> Ejemplo para borrar un usuario

```python
import requests

url = "http://localhost:3000/api/users/6267e1da2d182b1e3465b1fe"

payload={}
headers = {
  'Token': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MDk4MTU5NSwiZXhwIjoxNjUxNDEzNTk1fQ.Cm41J7_mgNitftVbilf5QGKTNLI9WTg1NXr3JZwt20I'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Token", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MDk4MTU5NSwiZXhwIjoxNjUxNDEzNTk1fQ.Cm41J7_mgNitftVbilf5QGKTNLI9WTg1NXr3JZwt20I");

var requestOptions = {
  method: 'DELETE',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("http://localhost:3000/api/users/6267e1da2d182b1e3465b1fe", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```shell
curl --location --request DELETE 'http://localhost:3000/api/users/6267e1da2d182b1e3465b1fe' \
--header 'Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNjdlMWRhMmQxODJiMWUzNDY1YjFmZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MDk4MTU5NSwiZXhwIjoxNjUxNDEzNTk1fQ.Cm41J7_mgNitftVbilf5QGKTNLI9WTg1NXr3JZwt20I'
```

> Si la ejecución ha sido correcta, veremos el siguiente mensaje JSON

```json
"User has been deleted"
```

Llamada mediante el método DELETE para poder borrar cualquier usuario mediante su "_id".

Al igual que en el anterior ejemplo, un administrador podrá borrar cualquier usuario, pero los usuarios normales solo se podrán borrar a sí mismos.

### HTTP Request
`DELETE http://localhost:3000/api/users/<user id>`

# Series

## Crear una serie

> Ejemplo de creación de una serie

```shell
curl --location --request POST 'http://localhost:3000/api/series/' \
--header 'Content-Type: application/json' \
--header 'Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNmE3ZmYzOGMxYWE4NmI2ZjkwMWVjYSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MTE0Njc2MSwiZXhwIjoxNjUxNTc4NzYxfQ.LCnnXahkb7WhmEu3t_1BWeBS_Y3m4HfgvEGMZfo_7ec' \
--data-raw '{
    "title": "Serie de pruebas",
    "desc": "Aquí va la descripción",
    "year": 2022
}'
```

```python
import requests
import json

url = "http://localhost:3000/api/series/"

payload = json.dumps({
  "title": "Serie de pruebas",
  "desc": "Aquí va la descripción",
  "year": 2022
})
headers = {
  'Content-Type': 'application/json',
  'Token': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNmE3ZmYzOGMxYWE4NmI2ZjkwMWVjYSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MTE0Njc2MSwiZXhwIjoxNjUxNTc4NzYxfQ.LCnnXahkb7WhmEu3t_1BWeBS_Y3m4HfgvEGMZfo_7ec'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");
myHeaders.append("Token", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNmE3ZmYzOGMxYWE4NmI2ZjkwMWVjYSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MTE0Njc2MSwiZXhwIjoxNjUxNTc4NzYxfQ.LCnnXahkb7WhmEu3t_1BWeBS_Y3m4HfgvEGMZfo_7ec");

var raw = JSON.stringify({
  "title": "Serie de pruebas",
  "desc": "Aquí va la descripción",
  "year": 2022
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("http://localhost:3000/api/series/", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> Una vez ejecutado correctamente, nos devolverá lo siguiente

```json
{
    "title": "Serie de pruebas",
    "desc": "Aquí va la descripción",
    "year": 2022,
    "seasons": [],
    "_id": "626a80558c1aa86b6f901ece",
    "createdAt": "2022-04-28T11:53:57.532Z",
    "updatedAt": "2022-04-28T11:53:57.532Z",
    "__v": 0
}
```

Para poder realizar este tipo de operaciones, vamos a necesitar ser un usuario administrador.

Por defecto, se pueden agregar los siguientes campos con los siguientes tipos de datos.

| Campo    | Tipo   | Descripción                                                        |
|----------|--------|--------------------------------------------------------------------|
| title    | String | Título a mostrar de la serie                                       |
| desc     | String | Descripción básica de la serie                                     |
| img      | String | Contiene la URL de la imagen                                       |
| imgTitle | String | Contiene la URL del logo de la serie                               |
| imgSm    | String | Contiene la URL de la miniatura de la serie                        |
| trailer  | String | Contiene la URL del tráiler de la serie                            |
| year     | Number | Contiene el año de estreno de la serie                             |
| limit    | Number | Edad mínima recomendada para ver la serie                          |
| genre    | String | Género principal de la serie                                       |
| seasons  | Array  | Contiene los id de las diferentes temporadas que la serie contiene |

De todos estos campos, el único requerido será el de "title", el cual además deberá ser único.

### HTTP Request
`POST http://localhost:3000/api/series/`
## Ver una serie

> Ejemplo para sacar la información de una serie

```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("http://localhost:3000/api/series/626a80558c1aa86b6f901ece", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python
import requests

url = "http://localhost:3000/api/series/626a80558c1aa86b6f901ece"

payload={}
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'http://localhost:3000/api/series/626a80558c1aa86b6f901ece'
```

> Nos devolverá el siguiente objeto

```json
{
    "_id": "626a80558c1aa86b6f901ece",
    "title": "Serie de pruebas",
    "desc": "Aquí va la descripción",
    "year": 2022,
    "seasons": [],
    "createdAt": "2022-04-28T11:53:57.532Z",
    "updatedAt": "2022-04-28T11:53:57.532Z",
    "__v": 0
}
```

Se trata de una llamada pública para la API, en este caso, no requiere ni inicio de sesión, siempre que se tenga un id de una serie, podemos consultar sus detalles.

El id de las series siempre será un parámetro único autogenerado por la base de datos al escribir la entrada, por lo que si no disponemos de esta clave, podemos optar por la opción de la siguiente llamada y ver todas las series con sus correspondientes claves.

### HTTP Request
`GET http://localhost:3000/api/series/<serie id>`
## Ver todas las series

> Ejemplo para ver todas las series disponibles

```shell
curl --location --request GET 'http://localhost:3000/api/series/all'
```

```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("http://localhost:3000/api/series/all", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python
import requests

url = "http://localhost:3000/api/series/all"

payload={}
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

> Nos devolverá un array con todas las series en forma de objeto

```json
[
    {
        "_id": "626a80558c1aa86b6f901ece",
        "title": "Serie de pruebas",
        "desc": "Aquí va la descripción",
        "year": 2022,
        "seasons": [],
        "createdAt": "2022-04-28T11:53:57.532Z",
        "updatedAt": "2022-04-28T11:53:57.532Z",
        "__v": 0
    }
]
```

Al igual que la llamada anterior, se trata de una llamada pública, la cual no requiere de inicio de sesión, por lo que se puede consultar directamente desde el navegador si se prefiere.

Mediante la información mostrada en las diferentes series, podremos filtrarlas diréctamente y buscar mediante la llamada anterior toda la información de una concreta.

### HTTP Request

`GET http://localhost:3000/api/series/all`
## Actualizar una serie

> Ejemplo de modificación de la serie creada anteriormente

```python
import requests

url = "http://localhost:3000/api/series/626a80558c1aa86b6f901ece"

payload = "{\r\n    \"title\": \"Serie actualizada\"\r\n}"
headers = {}

response = requests.request("PUT", url, headers=headers, data=payload)

print(response.text)
```

```javascript
var raw = "{\r\n    \"title\": \"Serie actualizada\"\r\n}";

var requestOptions = {
  method: 'PUT',
  body: raw,
  redirect: 'follow'
};

fetch("http://localhost:3000/api/series/626a80558c1aa86b6f901ece", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```shell
curl --location --request PUT 'http://localhost:3000/api/series/626a80558c1aa86b6f901ece' \
--data-raw '{
    "title": "Serie actualizada"
}'
```

> Si se ejecuta correctamente, veremos la información de la serie actualizada ya

```json
{
    "_id": "626a80558c1aa86b6f901ece",
    "title": "Serie actualizada",
    "desc": "Aquí va la descripción",
    "year": 2022,
    "seasons": [],
    "createdAt": "2022-04-28T11:53:57.532Z",
    "updatedAt": "2022-04-28T12:30:39.928Z",
    "__v": 0
}
```

Se trata de una llamada que solo los administradores pueden ejecutar, y sería similar a la creación de una serie, pero incluyendo en el cuerpo de la llamada los campos junto a los valores que se vayan a modificar.

### HTTP Request
`PUT http://localhost:3000/api/series/<series id>`

## Borrar una serie

> Ejemplo para borrar la serie creada anteriormente

```shell
curl --location --request DELETE 'http://localhost:3000/api/series/626a80558c1aa86b6f901ece'
```

```python
import requests

url = "http://localhost:3000/api/series/626a80558c1aa86b6f901ece"

payload={}
headers = {}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

```javascript
var requestOptions = {
  method: 'DELETE',
  redirect: 'follow'
};

fetch("http://localhost:3000/api/series/626a80558c1aa86b6f901ece", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> Si se ejecuta correctamente, nos devolverá el siguiente mensaje en JSON

```json
"Deleted succesfully"
```

Al igual que la anterior, es necesario ser usuario administrador para poder llevar a cabo esta llamada satisfactoriamente.

Estas llamadas serán principalmente para el área de administración de la página, por lo que no estarán visibles de cara al público.

### HTTP Request
`DELETE http://localhost/3000/api/series/<serie id>`
# Temporadas

## Crear una temporada

> Ejemplo para crear una temporada nueva

```javascript
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");
myHeaders.append("Token", "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNmE3ZmYzOGMxYWE4NmI2ZjkwMWVjYSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MTE0Njc2MSwiZXhwIjoxNjUxNTc4NzYxfQ.LCnnXahkb7WhmEu3t_1BWeBS_Y3m4HfgvEGMZfo_7ec");

var raw = JSON.stringify({
  "title": "Temporada de pruebas",
  "desc": "Aquí va la descripción",
  "serie": "1"
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("http://localhost:3000/api/seasons/", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python
import requests
import json

url = "http://localhost:3000/api/seasons/"

payload = json.dumps({
  "title": "Temporada de pruebas",
  "desc": "Aquí va la descripción",
  "serie": "1"
})
headers = {
  'Content-Type': 'application/json',
  'Token': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNmE3ZmYzOGMxYWE4NmI2ZjkwMWVjYSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MTE0Njc2MSwiZXhwIjoxNjUxNTc4NzYxfQ.LCnnXahkb7WhmEu3t_1BWeBS_Y3m4HfgvEGMZfo_7ec'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'http://localhost:3000/api/seasons/' \
--header 'Content-Type: application/json' \
--header 'Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYyNmE3ZmYzOGMxYWE4NmI2ZjkwMWVjYSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTY1MTE0Njc2MSwiZXhwIjoxNjUxNTc4NzYxfQ.LCnnXahkb7WhmEu3t_1BWeBS_Y3m4HfgvEGMZfo_7ec' \
--data-raw '{
    "title": "Temporada de pruebas",
    "desc": "Aquí va la descripción",
    "serie": "1"
}'
```

> Si se ejecuta correctamente, nos devolverá la información siguiente

```json
{
    "serie": "1",
    "episodes": [],
    "_id": "626a9aa88c1aa86b6f901ed5",
    "createdAt": "2022-04-28T13:46:16.165Z",
    "updatedAt": "2022-04-28T13:46:16.165Z",
    "__v": 0
}
```

Siguiendo el modelo con el que hemos descrito las temporadas dentro de nuestra base de datos, podemos crearlas utilizando los siguientes datos:

| Campo            | Tipo   | Descripción                                    |
|------------------|--------|------------------------------------------------|
| number           | Number | Número de temporada                            |
| serie            | String | Id de la serie a la que pertenece              |
| episodes         | Array  | Ids de los episodios que contiene la temporada |
| numberOfEpisodes | Number | Número de episodios que tiene la temporada     |

### HTTP Request
`POST http://localhost:3000/api/seasons/`

## Ver una temporada

> Ejemplo de llamada para ver información de una temporada

```shell
curl --location --request GET 'http://localhost:3000/api/seasons/626ab78c8c1aa86b6f901ed8'
```

```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("http://localhost:3000/api/seasons/626ab78c8c1aa86b6f901ed8", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python
import requests

url = "http://localhost:3000/api/seasons/626ab78c8c1aa86b6f901ed8"

payload={}
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

> Su ejecución nos devolverá la temporada correspondiente con el id de la url

```json
{
    "_id": "626ab78c8c1aa86b6f901ed8",
    "serie": "1",
    "episodes": [],
    "createdAt": "2022-04-28T15:49:32.673Z",
    "updatedAt": "2022-04-28T15:49:32.673Z",
    "__v": 0
}
```

Se trata de una llamada pública también, que no requiere de autenticación previa, y que podremos hacer siempre que sepamos el id único de la temporada a buscar.

En caso de no saber esta información, podemos optar por la siguiente llamada.

### HTTP Request
`GET http://localhost:3000/api/seasons/<id temporada>`
## Ver todas las temporadas

> Ejemplo para ver todas las temporadas creadas

```python
import requests

url = "http://localhost:3000/api/seasons/all"

payload={}
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("http://localhost:3000/api/seasons/all", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```shell
curl --location --request GET 'http://localhost:3000/api/seasons/all'
```

> Como resultado, nos devolverá un array con todas las temporadas que haya creadas

```json
[
    {
        "_id": "626a9aa88c1aa86b6f901ed5",
        "serie": "1",
        "episodes": [],
        "createdAt": "2022-04-28T13:46:16.165Z",
        "updatedAt": "2022-04-28T13:46:16.165Z",
        "__v": 0
    },
    {
        "_id": "626ab78c8c1aa86b6f901ed8",
        "serie": "2",
        "episodes": [],
        "createdAt": "2022-04-28T15:49:32.673Z",
        "updatedAt": "2022-04-28T15:49:32.673Z",
        "__v": 0
    }
]
```

Como respuesta, nos va a devolver un array con todos los objetos de temporadas que estén almacenadas en la base de datos.

Se puede realizar esta llamada sin necesidad de autenticarse.

### HTTP Request
`GET http://localhost:3000/api/seasons/all`
## Actualizar una temporada

> Ejemplo de actualización de una temporada

```shell
curl --location --request PUT 'http://localhost:3000/api/seasons/626a9aa88c1aa86b6f901ed5' \
--data-raw '{
    "title": "Serie actualizada"
}'
```

```javascript
var raw = "{\r\n    \"title\": \"Serie actualizada\"\r\n}";

var requestOptions = {
  method: 'PUT',
  body: raw,
  redirect: 'follow'
};

fetch("http://localhost:3000/api/seasons/626a9aa88c1aa86b6f901ed5", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python
import requests

url = "http://localhost:3000/api/seasons/626a9aa88c1aa86b6f901ed5"

payload = "{\r\n    \"title\": \"Serie actualizada\"\r\n}"
headers = {}

response = requests.request("PUT", url, headers=headers, data=payload)

print(response.text)
```

> Nos devolverá el objeto de la serie actualizada

```json
{
    "_id": "626a9aa88c1aa86b6f901ed5",
    "serie": "626aba728c1aa86b6f901ede",
    "episodes": [],
    "createdAt": "2022-04-28T13:46:16.165Z",
    "updatedAt": "2022-04-28T16:02:10.673Z",
    "__v": 0
}
```
## Borrar una temporada

# Episodios

## Crear un episodio

## Ver un episodio

## Ver todos los episodios

## Actualizar un episodio

## Borrar un episodio

# Películas

## Crear una película

## Ver una película

## Ver todas las películas

## Ver una película aleatoria

## Actualizar una película

## Borrar una película

# Listas

## Crear una lista

## Ver una lista

## Ver todas las listas

## Ver listas aleatorias

## Actualizar una lista

## Borrar una lista