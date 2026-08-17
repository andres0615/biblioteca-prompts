# Generar script para insertar records en la tabla productos

# Completar controlador para third party

## 1. Cargar skill

- Carga la skill `read-files-constraints `

## 2. Leer archivos necesarios

Lee los siguientes archivos:

Esquema de las tablas:

- `otros/db/products.sql`
- `otros/db/product_category.sql`
- `otros/db/product_status.sql`

Datos de las tablas:

- `otros/db/products_data.json`
- `otros/db/product_category_data.json`
- `otros/db/product_status_data.json`

## 3. Generar script sql

- Genera un script sql para insertar datos en la tabla products
- Generaras 20 records
- Solo usaras las categorias `Electrónica` y `Ropa`
- Usaras los status `Activo` y `Agotado`
- ningun producto debe superar el stock de 20
- Guardaras el sql en `otros/plan/14-08-26/insert-products.sql` que ya existe