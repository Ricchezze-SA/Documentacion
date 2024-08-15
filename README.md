# API para Clientes

# Table of Contents

- [About](#about)
- [Getting Started](#getting_started)
- [Error Codes](#errors)
- [Usage](#usage)

# About <a name = "about"></a>

<p style="font-size:18px">Guia de utilizacion de la api para clientes con ejemplos de uso (en AngularJS v18) y capturas de
respuestas en PostMan</p>

# Getting Started <a name = "getting_started"></a>

<p style="font-size:18px">Como prerequisito inicial van a necesitar ser dados de alta por el area de sistemas/comercial de la
empresa, la cual se les asignara un mail, contraseña y claveApi; siendo esta ultima para poder
realizar todas las consultas</p>

# Error Codes<a name = "errors"></a>

<p style="font-size:18px">Se listaran todos los codigos de error posible de cada metodo y su significado:

```diff

- ESTADO 1
# Este codigo indica que el call al endpoint resulto exitoso
- ESTADO 2
# Este codigo se debe a que se a que occurrio un error en el query
- ESTADO 3
# Este codigo se debe a que se indico mal el recurso, es decir el primer parametro inicial (productos/externos/etc)
- ESTADO 4
# Este codigo se debe a que se indico el recurso pero el segundo parametro es inexistente(get/foto)
- ESTADO 5
# Este codigo se debe a que se intento acceder a un metodo/funcion la cual no se tiene permisos para ese usuario
- ESTADO 9
# Este codigo se debe a una falla en el stock, acompañado de este ESTADO lo acompaña el/los productos con los cuales se tiene problema de stock

```

# Usage <a name = "usage"></a>

<p style="font-size:18px">A continuacion van a tener los ejemplos de uso para cada endpoint</p>

> Para cada consulta se requerira el envio de la clave api que se debera de hacer como
> encabezado(header):

```json
    {
   "KEY": Auth,
   "VALUE": '56c099b5f8bc89d0efa728fe3e8a8c3b'
    }
```

## GETS

### 1.Productos obtener todo:

<p style="font-size:18px">Con este endpoint van a poder obtener un listado completo de todos y cada uno de los productos con
todas sus caracteristicas</p>

- ***https://www.mueblesricchezze.com.ar/api/v2/productos/get*** :

```Js
  const headers = new HttpHeaders({ Auth: '56c099b5f8bc89d0efa728fe3e8a8c3b' });
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
  const headers = new HttpHeaders({ Auth: '56c099b5f8bc89d0efa728fe3e8a8c3b' });
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
solamente tendran que relacionar el producto con el COD_ALFA y utilizar como source el campo "foto"</p>

- ***https://www.mueblesricchezze.com.ar/api/v2/externos/foto/***

```Js
  const headers = new HttpHeaders({ Auth: '56c099b5f8bc89d0efa728fe3e8a8c3b' });
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
            "ARCHIVO": "30007415_001_01.jpg",
            "foto": "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30007415_001_01.jpg"
        },
        {
            "COD_ALFA": "30007415",
            "VERSION": "002",
            "ORDEN": "02",
            "FECHA": "1716552365",
            "DIR": "tana",
            "ARCHIVO": "30007415_002_02.jpg",
            "foto": "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30007415_002_02.jpg"
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
  const headers = new HttpHeaders({ Auth: '56c099b5f8bc89d0efa728fe3e8a8c3b' });
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
            "ARCHIVO": "30031528_001_01.jpg",
            "foto": "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30031528_001_01.jpg"
        },
        {
            "COD_ALFA": "30031528",
            "VERSION": "002",
            "ORDEN": "02",
            "FECHA": "1716552413",
            "DIR": "tana",
            "ARCHIVO": "30031528_002_02.jpg",
            "foto": "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30031528_002_02.jpg"
        },
        {
            "COD_ALFA": "30031528",
            "VERSION": "003",
            "ORDEN": "03",
            "FECHA": "1716552413",
            "DIR": "tana",
            "ARCHIVO": "30031528_003_03.jpg",
            "foto": "https://www.mueblesricchezze.com.ar/api/v2/dir_fotos/tana/30031528_003_03.jpg"
        }
    ]
}
```

#### POSTMAN GET ALL IMAGES OF ONE PRODUCT:

<img width="85%" src="./imgs/getAllimagesOneprod.png" />

<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>
<div style="width:100%; height:8px; background-color:#ff3e35; margin:-10px 0"></div>
<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>

## POSTS :

### 1.Enviar pedido :

<p style="font-size:18px">Para el envio de los pedidos se debe de indicar en el body de la request los siguientes datos con
esta misma estructura:</p>

```JSON
{
  "obs": "aqui va la observacion que vean conveniente",
  "productos":[{
    "cod_alfa": "xxxxxx",
    "cant" : "xx"
  },
  {...}...                                ---> SE ENVIAN TANTOS PRODUCTOS COMO SE DESEAN EN FORMA DE ARREGLO
  ]
}
```

- ***https://www.mueblesricchezze.com.ar/api/v2/externos***

```Js
const headers = new HttpHeaders({ Auth: '56c099b5f8bc89d0efa728fe3e8a8c3b' });
const order = {
  obs: "observacion",
    productos: [
        {
            cod_alfa: "35231773",
            cant: 10
        },

        {
            cod_alfa: "34231701",
            cant: 2
        }
    ]
}
  return this.http
    .post(`https://www.mueblesricchezze.com.ar/api/v2/externos`, JSON.stringify(order),{ headers })
    .subscribe({
      next: (res: any) => {
        console.info('ProductService ::: sendOrder ---> SUCCESS', res);
        return res
      },
    });

```

<p style="font-size:18px">Este codigo obtendra como resultado en el siguiente JSON</p>

```JSON
{
    "estado": 1,
    "mensaje": "Nota de venta enviada"
}
```

#### POSTMAN :

<img width="85%" src="./imgs/postNV.png" />

<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>
<div style="width:100%; height:5px; background-color:grey; margin:20px 0"></div>
