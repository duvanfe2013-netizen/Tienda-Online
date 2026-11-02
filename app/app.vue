<script setup>
import { ref } from 'vue'

const productos = ref([
  {
    id: 1,
    imagen: '/iphone-18-pro-titanio-natural.png',
    descripcion: 'iPhone 18 Pro: potencia profesional y diseño en titanio.',
    valor: 5499000,
    descuento: 10,
  },
  {
    id: 2,
    imagen: '/iphone-17-base-negro.png',
    descripcion: 'iPhone 17: rendimiento fluido y pantalla ultrabrillante.',
    valor: 4499000,
    descuento: 5,
  },
  {
    id: 3,
    imagen: '/phone-16-promax-titanio-natural.png',
    descripcion: 'iPhone 16 Pro Max: cámara avanzada y gran autonomía.',
    valor: 6299000,
    descuento: 15,
  },
  {
    id: 4,
    imagen: '/iphone-15-negro.png',
    descripcion: 'iPhone 15: cámara de 48 MP e Isla Dinámica.',
    valor: 3999000,
    descuento: 12,
  },
  {
    id: 5,
    imagen: '/airpods-pro.png',
    descripcion: 'AirPods Pro 2: audio espacial y cancelación de ruido.',
    valor: 1199000,
    descuento: 8,
  },
  {
    id: 6,
    imagen: '/airpods-max.png',
    descripcion: 'AirPods Max: sonido de alta fidelidad y diseño premium.',
    valor: 2499000,
    descuento: 0,
  },
  {
    id: 7,
    imagen: '/magsafe-charger.png',
    descripcion: 'Cargador MagSafe para una carga inalámbrica práctica.',
    valor: 249000,
    descuento: 0,
  },
  {
    id: 8,
    imagen: '/adapter-20w.png',
    descripcion: 'Adaptador de corriente USB-C de 20 W.',
    valor: 119000,
    descuento: 0,
  },
  {
    id: 9,
    imagen: '/finewoven-case.png',
    descripcion: 'Funda FineWoven con ajuste preciso para iPhone.',
    valor: 299000,
    descuento: 0,
  },
  {
    id: 10,
    imagen: '/airtag.png',
    descripcion: 'AirTag para localizar tus objetos personales.',
    valor: 149000,
    descuento: 0,
  },
])
</script>

<template>
  <main class="collection-section">
    <header class="section-heading">
      <div>
        <p class="section-kicker">La selección</p>
        <h1>Un mundo de posibilidades.</h1>
      </div>
      <p class="section-description">Tecnología que inspira.<br>Diseño que permanece.</p>
    </header>

    <section class="product-grid" aria-label="Catálogo de productos">
      <article v-for="producto in productos" :key="producto.id" class="product-card">
        <img :src="producto.imagen" :alt="producto.descripcion">
        <h2>{{ producto.descripcion }}</h2>
        <p>{{ producto.valor }} COP</p>
      </article>
    </section>
  </main>
</template>
