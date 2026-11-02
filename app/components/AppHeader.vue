<script setup>
defineProps({
  nombreTienda: {
    type: String,
    required: true,
  },
  cantidadItems: {
    type: Number,
    default: 0,
  },
  categoriaActiva: {
    type: String,
    default: 'todos',
  },
})

const emit = defineEmits(['ver-carrito', 'cambiar-categoria'])

const categorias = [
  { etiqueta: 'Tienda', valor: 'todos' },
  { etiqueta: 'iPhone', valor: 'iphone' },
  { etiqueta: 'Audio', valor: 'audio' },
  { etiqueta: 'Accesorios', valor: 'accesorios' },
]
</script>

<template>
  <header class="global-nav">
    <a class="brand-mark" href="#" :aria-label="`${nombreTienda} — inicio`">
      <svg viewBox="0 0 18 22" aria-hidden="true">
        <path d="M14.8 11.7c0-2 1.6-3 1.7-3.1a4 4 0 0 0-3.2-1.7c-1.4-.2-2.7.8-3.4.8-.7 0-1.8-.8-3-.8a4.5 4.5 0 0 0-3.8 2.3c-1.6 2.8-.4 6.9 1.1 9.1.7 1.1 1.5 2.2 2.6 2.2 1 0 1.4-.7 2.7-.7s1.7.7 2.8.7 1.8-1 2.4-2.1a9.5 9.5 0 0 0 1.1-2.4 3.8 3.8 0 0 1-2-4.3ZM12.4 5.3A4 4 0 0 0 13.3 2a4.2 4.2 0 0 0-2.9 1.5 3.8 3.8 0 0 0-1 3.2 3.6 3.6 0 0 0 3-1.4Z" fill="currentColor" />
      </svg>
    </a>

    <nav class="main-links" aria-label="Categorías de productos">
      <button
        v-for="categoria in categorias"
        :key="categoria.valor"
        type="button"
        :class="{ 'is-active': categoriaActiva === categoria.valor }"
        :aria-current="categoriaActiva === categoria.valor ? 'page' : undefined"
        @click="emit('cambiar-categoria', categoria.valor)"
      >
        {{ categoria.etiqueta }}
      </button>
    </nav>

    <button class="cart-trigger" aria-label="Abrir carrito" @click="emit('ver-carrito')">
      <svg viewBox="0 0 20 20" aria-hidden="true">
        <path d="M3.3 6.4h13.4l-.9 10.1H4.2L3.3 6.4ZM7 7V5a3 3 0 0 1 6 0v2" fill="none" stroke="currentColor" stroke-width="1.3" stroke-linecap="round" stroke-linejoin="round" />
      </svg>
      <span v-if="cantidadItems" class="cart-count">{{ cantidadItems }}</span>
    </button>
  </header>

  <div class="announcement">
    <p>Un universo de posibilidades. Descubre la nueva generación de iPhone. <a href="#catalogo">Explorar ahora <span aria-hidden="true">›</span></a></p>
  </div>
</template>
