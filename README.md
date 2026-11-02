# Tienda virtual por componentes — Vue 3

Tienda de productos Apple desarrollada con Vue 3, Composition API y `<script setup>`. El proyecto conserva el diseño visual de la tienda original y organiza la comunicación entre componentes mediante props y emits.

## Requisitos

- Node.js LTS
- npm

## Instalación y ejecución

```bash
npm install
npm run dev
```

Abre la dirección que indique Nuxt, normalmente `http://localhost:3000`.

Para validar la compilación de producción:

```bash
npm run build
```

## Componentes y comunicación

El estado compartido (`productos`, `carrito`, visibilidad de la factura y consecutivo) se mantiene en `app/app.vue`.

| Componente | Responsabilidad |
|---|---|
| `AppHeader` | Recibe el nombre de la tienda y la cantidad de unidades; emite `ver-carrito`. |
| `ListaProductos` | Recibe el catálogo, renderiza tarjetas y reenvía `agregar-al-carrito` como `agregar-producto`. |
| `ProductoCard` | Recibe un producto, calcula el precio descontado con `computed` y emite `agregar-al-carrito`. |
| `CarritoCompra` | Presenta productos y totales; emite `incrementar`, `decrementar`, `eliminar` y `finalizar-compra`. |
| `FacturaCompra` | Recibe artículos, consecutivo y fecha; emite `nueva-compra`. |
| `AppFooter` | Presenta el nombre de la tienda, el año y el contacto. |

El catálogo contiene diez productos y seis tienen descuentos. Los precios se presentan con formato COP. La factura incluye el subtotal, los descuentos, el IVA del 19 % calculado sobre el subtotal descontado y el total a pagar.

## Verificación manual

1. Revisa que el catálogo muestre al menos ocho productos y que cinco o más tengan etiqueta de descuento, precio original y precio final.
2. Agrega dos veces el mismo producto: debe mantenerse una sola línea en el carrito y aumentar su cantidad y el contador del encabezado.
3. En el carrito, aumenta y disminuye cantidades; usa **Eliminar** y verifica que al quitar el último producto aparezca el estado vacío y **Finalizar compra** quede deshabilitado.
4. Agrega productos con y sin descuento; comprueba el subtotal, el total de descuentos y el total del carrito.
5. Finaliza una compra y comprueba el detalle de la factura, el consecutivo, la fecha, los descuentos, el IVA del 19 % y el total.
6. Selecciona **Nueva compra**: el carrito debe vaciarse, la factura debe ocultarse y el siguiente consecutivo debe aumentar en uno.
7. Revisa la interfaz en anchos de celular, tableta y escritorio.

## Avance por fases

El historial Git registra el desarrollo de esta copia en los commits:

1. Preparar el proyecto y catálogo inicial.
2. Crear componentes de presentación.
3. Conectar props y eventos entre componentes.
4. Completar carrito y cálculos de descuentos.
5. Generar factura con descuentos e IVA.
6. Documentar y validar la tienda.

La sustentación en video se debe grabar y compartir por separado; agrega aquí su enlace cuando esté disponible.
