# API para Clientes

# Table of Contents

- [About](#about)
- [Getting Started](#getting_started)
- [Error Codes](#errors)
- [Usage](#usage)

# About <a name = "about"></a>

<p style="font-size:18px">Esta API ha sido desarrollada para permitir a los clientes consultar detalles de los productos de forma instantánea, con valores en tiempo real. Incluye ejemplos de uso en AngularJS v18 y respuestas en Postman.</p>

# Getting Started <a name = "getting_started"></a>

<p style="font-size:18px">Como requisito previo, es necesario que el área de Sistemas o Comercial de la empresa les registre y les asigne un correo electrónico y una contraseña. Con estas credenciales, podrán iniciar sesión y obtener su token de autenticación.</p>

# Error Codes<a name = "errors"></a>

<p style="font-size:18px">Se listaran todos los codigos de error posible de cada metodo y su significado:

```diff

- ESTADO 1
# Este codigo indica que el call al endpoint resulto exitoso
- ESTADO 2
# Este codigo indica que el call al endpoint resulto exitoso pero no se obtuvieron resultados
- ESTADO 4
# Este codigo indica el vencimiento del token, se requiere solicitar/generar uno nuevo
- ESTADO 5
# Este codigo indica la ausencia del token en la call
- ESTADO 6
# Este codigo indica que el rol del usuario no esta autorizado para realizar dicha llamada
- ESTADO 7
# Este codigo indica un error de parametros
- ESTADO 8
# Este codigo indica un estado de error general, es utilizado como multiproposito para errores varios o no manejables con otro codigo
- ESTADO 9
# Este codigo se debe a una falla en el stock, acompañado de este ESTADO lo acompaña el/los productos con los cuales se tiene problema de stock

```

> Ante la aparicion de algun error no esperado comunicarse con el area de sistemas

# Usage <a name = "usage"></a>

<p style="font-size:18px">A continuacion van a tener los ejemplos de uso para cada endpoint</p>

> Para cada consulta se requerira el envio del token que se debera de hacer como
> encabezado(header) el cual se obtiene luego de hacer el log in:

## LogIn

Metodo Post

- ***https://www.mueblesricchezze.com.ar/api/v2/usuarios/login***

```ts
    async login(user: any): Promise<any> {
    const url = `https://www.mueblesricchezze.com.ar/api/v2/usuarios/login`;
    const headers = new HttpHeaders({ 'Content-Type': 'application/json' });

    return lastValueFrom(
      this.http.post(url, user, { headers }).pipe(
        tap({
          next: (response: any) => {
            console.log(response);
            return response;
          },
        })
      )
    )
  }
```

<p style="font-size:18px">Este codigo obtendra como resultado en el siguiente JSON</p>

```JSON
{
    "estado": 1,
    "mensaje": "Inicio de sesión exitoso",
    "usuario": "PEPE GRILLO",
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZFVzdWFyaW8iOjkwNywiaWRWZW5kZWRvciI6OTA3sCJpZENsaWVudGUiOm51bGwsIm5vbWJyZSI6IlBFUEUgR1JJTExPIiwicm9sIjoiQURNSU4iLCJjbGF2ZUFwaSI6IjNkMjM1MDEzZDRhNzgzYjg2Zjc5ZjFhNjg0ZDYyZjk0IiwiY29ycmVvIjoiZ3JpbGxvQHRlc3QuY29tIiwiZmVjaGFfYWx0YSI6IjIwMjQtMDkxSdAiLCJob3JhIjoiMDg6NTk6NDgiLCJpYXQiOjE3NDIyMTU1MTQsImV4cCI6MTc0MjM0NTExNH0.fOQKzOL1yNQfr2J5Ox20tLCIB65Heqj-sJXsj818cz4"
}

```

#### POSTMAN LOGIN:

<img width="85%" src="./imgs/logIn.png" />

<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>
<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>

```json
    {
   "KEY": Auth,
   "VALUE": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZFVzdWFyaW8iOjkwNywiaWRWZW5kZWRvciI6OTA3LCJpZENsaWVudGUiOm51bGwsIm5vbWJyZSI6IlBFUEUgR1JJTExPIiwicm9sIjoiQURNSU4iLCJjbGF2ZUFwaSI6IjNkMjM1MDEzZDRhNzgzYjg2Zjc5ZjFhNjg0ZDYyZjk0IiwiY29ycmVvIjoiZ3JpbGxvQHRlc3QuY29tIiwiZmVjaGFfYWx0YSI6IjIwMjQtMDktMzAiLCJob3JhIjoiMDg6NTk6NDgiLCJpYXQiOjE3NDIyMTU1MTQsImV4cCI6MTc0MjM0NTExNH0.fOQKzOL1yNQfr2J5Ox20tLCIB65Heqj-sJXsj818cz4"
    }
```

`el token mostrado en esta documentacion es ficticio a modo de ejemplo`

## GETS

### 1.Productos obtener todo:

<p style="font-size:18px">Con este endpoint van a poder obtener un listado completo de todos y cada uno de los productos con
todas sus caracteristicas</p>

- ***https://www.mueblesricchezze.com.ar/api/v2/productos/get***

```Js
  PRODUCCION
  const headers = new HttpHeaders({ Auth: 'eyJ0eXAiOiJKV1QiLCJh...' });
  return this.http
    .get(`https://www.mueblesricchezze.com.ar/api/v2/productos/get`, { headers })
    .subscribe({
      next: (prods: any) => {
        console.info('ProductService ::: getProducts ---> SUCCESS', prods);
        return prods
      },
    });
```

<p style="font-size:18px">Este codigo obtendra como resultado en el siguiente JSON</p>

```JSON
{
  "estado": 1,
  "datos": [
      {
          "COD_ALFA": "30031528",
          "CODIGO": "261633062101",
          "DETALLE": "PLACARD TANA ECO 2P CORR FRESNO BLANCO",
          "RUBRO": "TANA_ECO",
          "ORDEN_RUBRO": "151",
          "SUBRUBRO": "PLACARD 2 PUERTAS CORREDIZAS",
          "ORDEN_SUBRUBRO": "20",
          "BULTOS": "2.00",
          "ALTO": "181.70",
          "ANCHO": "112.80",
          "PROFUNDIDA": "54.00",
          "PESO": "77.00",
          "FOTO": "tana",
          "DISPONIBLE": "193",
          "ACTUALIZAD": "18/06/2024",
          "HORA": "13:14:47"
      },
      {
          "COD_ALFA": "30031628",
          "CODIGO": "261633062102",
          "DETALLE": "PLACARD TANA ECO 3P CORR FRESNO BLANCO",
          "RUBRO": "TANA_ECO",
          "ORDEN_RUBRO": "151",
          "SUBRUBRO": "PLACARD 3 PUERTAS CORREDIZAS",
          "ORDEN_SUBRUBRO": "35",
          "BULTOS": "3.00",
          "ALTO": "181.50",
          "ANCHO": "169.50",
          "PROFUNDIDA": "54.00",
          "PESO": "110.50",
          "FOTO": "tana",
          "DISPONIBLE": "126",
          "ACTUALIZAD": "18/06/2024",
          "HORA": "13:14:47"
      },
      ...
      ]
}
```

#### POSTMAN GET ALL PRODUCTS:

<img width="85%" src="./imgs/getAllprods.png" />

<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>
<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>

### 2.Productos obtener uno(1):

<p style="font-size:18px">Este les va permitir obstener un unico producto indicandole su **COD_ALFA** como se muestra</p>

- ***https://www.mueblesricchezze.com.ar/api/v2/productos/get/:codalfa***

```Js
  PRODUCCION
  const headers = new HttpHeaders({ Auth: 'eyJ0eXAiOiJKV1QiLCJh...' });
  return this.http
    .get(`https://www.mueblesricchezze.com.ar/api/v2/productos/get/30031528`, { headers })
    .subscribe({
      next: (prods: any) => {
        console.info('ProductService ::: getOneProduct ---> SUCCESS', prods);
        return prods
      },
    });
```

<p style="font-size:18px">Este codigo obtendra como resultado en el siguiente JSON</p>

```JSON
{
  "estado": 1,
  "datos": [
      {
          "COD_ALFA": "30031528",
          "CODIGO": "261633062101",
          "DETALLE": "PLACARD TANA ECO 2P CORR FRESNO BLANCO",
          "RUBRO": "TANA_ECO",
          "ORDEN_RUBRO": "151",
          "SUBRUBRO": "PLACARD 2 PUERTAS CORREDIZAS",
          "ORDEN_SUBRUBRO": "20",
          "BULTOS": "2.00",
          "ALTO": "181.70",
          "ANCHO": "112.80",
          "PROFUNDIDA": "54.00",
          "PESO": "77.00",
          "FOTO": "tana",
          "DISPONIBLE": "193",
          "ACTUALIZAD": "18/06/2024",
          "HORA": "13:14:47"
      }
  ]
}
```

#### POSTMAN GET ONE PRODUCT:

<img width="85%" src="./imgs/getOneprods.png" />

<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>
<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>

### 2.Productos obtener imagenes:

<p style="font-size:18px">Este endpoint les entregara un arreglo de objetos con las imagenes de todos los productos, aqui
solamente tendran que relacionar el producto con el COD_ALFA y utilizar como source el campo "ARCHIVO"</p>

- ***https://www.mueblesricchezze.com.ar/api/v2/externos/foto/***

```Js
  PRODUCCION
  const headers = new HttpHeaders({ Auth: 'eyJ0eXAiOiJKV1QiLCJh...' });
  return this.http
    .get(`https://www.mueblesricchezze.com.ar/api/v2/externos/foto`, { headers })
    .subscribe({
      next: (imgs: any) => {
        console.info('ProductService ::: GetImages ---> SUCCESS', imgs);
        return imgs
      },
    });
```

<p style="font-size:18px">Este codigo obtendra como resultado en el siguiente JSON</p>

```JSON
{
  "estado": 1,
    "datos": [
        {
            "COD_ALFA": "30007415",
            "VERSION": "001",
            "ORDEN": "01",
            "FECHA": "1716552363",
            "DIR": "tana",
            "ARCHIVO": "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30007415_001_01.jpg"
        },
        {
            "COD_ALFA": "30007415",
            "VERSION": "002",
            "ORDEN": "02",
            "FECHA": "1716552365",
            "DIR": "tana",
            "ARCHIVO":  "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30007415_002_02.jpg"
        },
        ...
    ]
}
```

#### POSTMAN GET ALL IMAGES:

<img width="85%" src="./imgs/getAllimages.png" />

<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>
<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>

### 3.Productos obtener imagenes (un producto):

<p style="font-size:18px">Este les entregara el conjunto de imagenes de un unico producto como se indica debajo</p>

- ***https://www.mueblesricchezze.com.ar/api/v2/externos/foto/:codalfa***

```Js
  PRODUCCION
  const headers = new HttpHeaders({ Auth: 'eyJ0eXAiOiJKV1QiLCJh...' });
  return this.http
    .get(`https://www.mueblesricchezze.com.ar/api/v2/externos/foto/30031528`, { headers })
    .subscribe({
      next: (imgs: any) => {
        console.info('ProductService ::: GetImages ---> SUCCESS', imgs);
        return imgs
      },
    });
```

<p style="font-size:18px">Este codigo obtendra como resultado en el siguiente JSON</p>

```JSON
{
    "estado": 1,
    "datos": [
        {
            "COD_ALFA": "30031528",
            "VERSION": "001",
            "ORDEN": "01",
            "FECHA": "1716552413",
            "DIR": "tana",
            "ARCHIVO": "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30031528_001_01.jpg"
        },
        {
            "COD_ALFA": "30031528",
            "VERSION": "002",
            "ORDEN": "02",
            "FECHA": "1716552413",
            "DIR": "tana",
            "ARCHIVO": "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30031528_002_02.jpg"
        },
        {
            "COD_ALFA": "30031528",
            "VERSION": "003",
            "ORDEN": "03",
            "FECHA": "1716552413",
            "DIR": "tana",
            "ARCHIVO": "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30031528_003_03.jpg"
        }
    ]
}
```

#### POSTMAN GET ALL IMAGES OF ONE PRODUCT:

<img width="85%" src="./imgs/getAllimagesOneprod.png" />

<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>
<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>
