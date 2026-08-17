# Completar controlador para categorias

## 1. Cargar skill

- Carga la skill `read-files-constraints `

## 2. Leer archivos necesarios

Lee los siguientes archivos:

Archivos generales:

- `routes/api.php`

Archivos correspondientes al modulo productos:

- `app/Http/Controllers/ProductController.php`

Archivos correspondientes al modulo categorias:

- `otros/db/product_category.sql`
- `app/Models/ProductCategory.php`
- `app/Http/Controllers/ProductCategoryController.php`
- `app/Http/Requests/StoreProductCategoryRequest.php`
- `app/Http/Requests/UpdateProductCategoryRequest.php`

# 3. Generar plan para completar el controlador de categorias

- Basandote en el esquema y las convenciones de los archivos del modulo de productos, generaras un plan para completar el controlador de categorias `ProductCategoryController.php`
- El metodo `index` del controlador ya esta creado, no es necesario crearlo

# 4. Agregar las rutas al archivo `routes/api.php`

- Agrega las rutas correspondientes en `routes/api.php`
