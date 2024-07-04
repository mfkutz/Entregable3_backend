Con base en nuestra implementación actual de productos, modificar el método GET / para que cumpla con los siguientes puntos:

- Deberá poder recibir por query params un limit (opcional), una page (opcional), un sort (opcional) y un query (opcional)

- "limit" permitirá devolver sólo el número de elementos solicitados al momento de la petición, en caso de no recibir limit, éste será de 10. ✅<br>

  `http://localhost:8080/api/products`<br>

  `http://localhost:8080/api/products?limit=2`

- "page" permitirá devolver la página que queremos buscar, en caso de no recibir page, ésta será de 1. ✅<br>

`http://localhost:8080/api/products?limit=2&page=3`

control en caso de introducir una pagina inexistente<br>

`http://localhost:8080/api/products?page=4000`

- query, el tipo de elemento que quiero buscar (es decir, qué filtro aplicar), en caso de no recibir query, realizar la búsqueda general ✅

Aqui la disponibilidad depende del STOCK DISPONIBLE, true o false<br>

`http://localhost:8080/api/products?available=false`<br>

`http://localhost:8080/api/products?category=category1`

- sort: asc/desc, para realizar ordenamiento ascendente o descendente por precio, en caso de no recibir sort, no realizar ningún ordenamiento ✅

http://localhost:8080/api/products?sort=asc

- El método GET deberá devolver un objeto con el siguiente formato:
  {
  status:success/error
  payload: Resultado de los productos solicitados
  totalPages: Total de páginas
  prevPage: Página anterior
  nextPage: Página siguiente
  page: Página actual
  hasPrevPage: Indicador para saber si la página previa existe
  hasNextPage: Indicador para saber si la página siguiente existe.
  prevLink: Link directo a la página previa (null si hasPrevPage=false)
  nextLink: Link directo a la página siguiente (null si hasNextPage=false)
  }✅

-Se deberá poder buscar productos por categoría o por disponibilidad, y se deberá poder realizar un ordenamiento de
estos productos de manera ascendente o descendente por precio. ✅

Además, agregar al router de carts los siguientes endpoints:

- DELETE api/carts/:cid/products/:pid deberá eliminar del carrito el producto seleccionado.✅<br>

`http://localhost:8080/api/carts/65d7e7b7fbde72ff1ca1331c/products/65d79970965a8c28cd22b3b7`

- PUT api/carts/:cid deberá actualizar el carrito con un arreglo de productos con el formato especificado arriba.✅<br>

`http://localhost:8080/api/carts/6685f5d09ba15fe24bd9c61b`

ejemplo :<br>

_{
"products": [
{ "product": "667f3d1fa6b48d22023c4653", "quantity": 2 },
{ "product": "667ffa9419eebb369d37b872", "quantity": 1 },
{ "product": "6685e50fc7b02ca746d3b7e3", "quantity": 3 }
]
}_

- PUT api/carts/:cid/products/:pid deberá poder actualizar SÓLO la cantidad de ejemplares del
  producto por cualquier cantidad pasada desde req.body<br>

`http://localhost:8080/api/carts/6685f5d09ba15fe24bd9c61b/products/667ffab019eebb369d37b876`

Aqui le hice un pequeño control de stock, si ponemos mas del stock existente saldrá un error<br>
_{
"quantity":300
}_

- DELETE api/carts/:cid deberá eliminar todos los productos del carrito<br>

`http://localhost:8080/api/carts/6685f5d09ba15fe24bd9c61b`

- Esta vez, para el modelo de Carts, en su propiedad products, el id de cada producto generado dentro del
  array tiene que hacer referencia al modelo de Products. Modificar la ruta /:cid para que al traer todos
  los productos, los traiga completos mediante un “populate”. De esta manera almacenamos sólo el Id, pero
  al solicitarlo podemos desglosar los productos asociados.✅

- Crear una vista en el router de views ‘/products’ para visualizar todos los productos con su respectiva paginación. OPCIONAL (No realizado)

- Contar con el botón de “agregar al carrito” directamente, sin necesidad de abrir una página adicional con los detalles del producto. OPCIONAL (No realizado)

- Además, agregar una vista en ‘/carts/:cid (cartId) para visualizar un carrito específico, donde se deberán listar SOLO los productos que pertenezcan a dicho carrito. OPCIONAL (No realizado)

## Dependencies

- [express](https://www.npmjs.com/package/express) "^4.19.2" - Web framework for Node.js.
- [express-handlebars](https://www.npmjs.com/package/express-handlebars) "^7.1.2" - Template engine for Express based on Handlebars.
- [handlebars](https://www.npmjs.com/package/handlebars) "^4.7.8" - Mustache-like templating engine.
- [mongoose](https://www.npmjs.com/package/mongoose) "^8.4.4" - Elegant MongoDB object modeling for Node.js.
- [mongoose-paginate-v2](https://www.npmjs.com/package/mongoose-paginate-v2) "^1.8.2" - Pagination plugin for Mongoose.
- [nodemon](https://www.npmjs.com/package/nodemon) "^3.1.3" - Tool that automatically restarts the server when file changes are detected.
- [socket.io](https://www.npmjs.com/package/socket.io) "^4.7.5" - Library for real-time communication based on WebSockets.
