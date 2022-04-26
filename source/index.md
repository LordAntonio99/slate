---
title: Pumpum API

language_tabs: # must be one of https://prismjs.com/#supported-languages
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

## Ver todos los usuarios

## Actualizar un usuario

## Borrar un usuario

# Series

## Crear una serie

## Ver una serie

## Ver todas las series

## Actualizar una serie

## Borrar una serie

# Temporadas
# Episodios
# Películas
# Listas

