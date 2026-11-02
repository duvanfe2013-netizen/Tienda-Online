<script setup>
import { ref } from 'vue'
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
</script>

<template>
  <div class="store-shell">
    <AppHeader nombre-tienda="Apple Store" :cantidad-items="0" />
    <main>
      <HeroBanner :producto="productos[0]" />
      <ListaProductos :productos="productos" />
    </main>
    <AppFooter nombre-tienda="Apple Store" :anio="2026" contacto="Contacto" />
  </div>
</template>
