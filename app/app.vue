<script setup>
import { computed, ref } from 'vue'
import AppFooter from './components/AppFooter.vue'
import AppHeader from './components/AppHeader.vue'
import HeroBanner from './components/HeroBanner.vue'
import ListaProductos from './components/ListaProductos.vue'

const productos = ref([
  {
    id: 1,
    imagen: '/iphone-18-pro-titanio-natural.png',
    descripcion: 'iPhone 18 Pro: potencia profesional y diseño en titanio.',
    valor: 5499000,
    descuento: 10,
    categoria: 'iphone',
  },
  {
    id: 2,
    imagen: '/iphone-17-base-negro.png',
    descripcion: 'iPhone 17: rendimiento fluido y pantalla ultrabrillante.',
    valor: 4499000,
    descuento: 5,
    categoria: 'iphone',
  },
  {
    id: 3,
    imagen: '/phone-16-promax-titanio-natural.png',
    descripcion: 'iPhone 16 Pro Max: cámara avanzada y gran autonomía.',
    valor: 6299000,
    descuento: 15,
    categoria: 'iphone',
  },
  {
    id: 4,
    imagen: '/iphone-15-negro.png',
    descripcion: 'iPhone 15: cámara de 48 MP e Isla Dinámica.',
    valor: 3999000,
    descuento: 12,
    categoria: 'iphone',
  },
  {
    id: 5,
    imagen: '/airpods-pro.png',
    descripcion: 'AirPods Pro 2: audio espacial y cancelación de ruido.',
    valor: 1199000,
    descuento: 8,
    categoria: 'audio',
  },
  {
    id: 6,
    imagen: '/airpods-max.png',
    descripcion: 'AirPods Max: sonido de alta fidelidad y diseño premium.',
    valor: 2499000,
    descuento: 0,
    categoria: 'audio',
  },
  {
    id: 7,
    imagen: '/magsafe-charger.png',
    descripcion: 'Cargador MagSafe para una carga inalámbrica práctica.',
    valor: 249000,
    descuento: 0,
    categoria: 'accesorios',
  },
  {
    id: 8,
    imagen: '/adapter-20w.png',
    descripcion: 'Adaptador de corriente USB-C de 20 W.',
    valor: 119000,
    descuento: 0,
    categoria: 'accesorios',
  },
  {
    id: 9,
    imagen: '/finewoven-case.png',
    descripcion: 'Funda FineWoven con ajuste preciso para iPhone.',
    valor: 299000,
    descuento: 0,
    categoria: 'accesorios',
  },
  {
    id: 10,
    imagen: '/airtag.png',
    descripcion: 'AirTag para localizar tus objetos personales.',
    valor: 149000,
    descuento: 0,
    categoria: 'accesorios',
  },
])

const carrito = ref([])
const categoriaActiva = ref('todos')
const mostrarCarrito = ref(false)

const productosVisibles = computed(() => categoriaActiva.value === 'todos'
  ? productos.value
  : productos.value.filter(producto => producto.categoria === categoriaActiva.value))

const cantidadItems = computed(() => carrito.value.reduce(
  (total, item) => total + item.cantidad,
  0,
))

function agregarProducto(producto) {
  const itemExistente = carrito.value.find(item => item.producto.id === producto.id)

  if (itemExistente) {
    itemExistente.cantidad += 1
    return
  }

  carrito.value.push({ producto, cantidad: 1 })
}

function cambiarCategoria(categoria) {
  categoriaActiva.value = categoria
  window.scrollTo({ top: 600, behavior: 'smooth' })
}

function cambiarCantidad(id, cambio) {
  const item = carrito.value.find(producto => producto.producto.id === id)
  if (!item) return

  item.cantidad += cambio
  if (item.cantidad <= 0) {
    carrito.value = carrito.value.filter(producto => producto.producto.id !== id)
  }
}

function formatearMoneda(valor) {
  return new Intl.NumberFormat('es-CO', {
    style: 'currency',
    currency: 'COP',
    maximumFractionDigits: 0,
  }).format(valor)
}
</script>

<template>
  <div class="store-shell">
    <AppHeader
      nombre-tienda="Apple Store"
      :cantidad-items="cantidadItems"
      :categoria-activa="categoriaActiva"
      @cambiar-categoria="cambiarCategoria"
      @ver-carrito="mostrarCarrito = true"
    />
    <main>
      <HeroBanner :producto="productos[0]" />
      <ListaProductos
        :productos="productosVisibles"
        @agregar-producto="agregarProducto"
      />
    </main>
    <AppFooter nombre-tienda="Apple Store" :anio="2026" contacto="Contacto" />

    <div v-if="mostrarCarrito" class="cart-overlay" @click.self="mostrarCarrito = false">
      <aside class="cart-drawer" role="dialog" aria-modal="true" aria-labelledby="cart-title">
        <div class="cart-heading">
          <div>
            <p class="section-kicker">Tu selección</p>
            <h2 id="cart-title">Tu bolsa</h2>
          </div>
          <button class="cart-close" aria-label="Cerrar carrito" @click="mostrarCarrito = false">×</button>
        </div>
        <div class="cart-content">
          <table v-if="carrito.length" class="cart-table">
            <thead>
              <tr>
                <th scope="col">Producto</th>
                <th scope="col">Precio</th>
                <th scope="col">Cantidad</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in carrito" :key="item.producto.id">
                <td>
                  <div class="cart-product">
                    <img :src="item.producto.imagen" :alt="item.producto.descripcion">
                    <strong>{{ item.producto.descripcion }}</strong>
                  </div>
                </td>
                <td>{{ formatearMoneda(item.producto.valor) }}</td>
                <td>
                  <div class="quantity-control">
                    <button
                      :aria-label="`Disminuir cantidad de ${item.producto.descripcion}`"
                      @click="cambiarCantidad(item.producto.id, -1)"
                    >
                      −
                    </button>
                    <span>{{ item.cantidad }}</span>
                    <button
                      :aria-label="`Aumentar cantidad de ${item.producto.descripcion}`"
                      @click="cambiarCantidad(item.producto.id, 1)"
                    >
                      +
                    </button>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
          <div v-else class="cart-empty">
            <span class="empty-bag-icon" aria-hidden="true">⌑</span>
            <h3>Tu bolsa está esperando.</h3>
            <p>Descubre algo extraordinario para ti.</p>
          </div>
        </div>
      </aside>
    </div>
  </div>
</template>
