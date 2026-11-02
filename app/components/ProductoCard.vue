<script setup>
import { computed } from 'vue'

const props = defineProps({
  producto: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['agregar-al-carrito'])

const valorConDescuento = computed(() => Math.round(
  props.producto.valor * (1 - props.producto.descuento / 100),
))

const formatoMoneda = new Intl.NumberFormat('es-CO', {
  style: 'currency',
  currency: 'COP',
  maximumFractionDigits: 0,
})
</script>

<template>
  <article class="product-card bg-gradient-to-b from-neutral-900/90 to-neutral-950 border border-neutral-800/80 rounded-2xl shadow-xl">
    <div class="product-card-image h-56 w-full flex items-center justify-center overflow-hidden p-4">
      <span v-if="producto.descuento > 0" class="offer-badge">-{{ producto.descuento }}%</span>
      <div v-if="producto.descuento > 0" class="product-card-offer-price">
        <span class="original-price">{{ formatoMoneda.format(producto.valor) }}</span>
        <strong>{{ formatoMoneda.format(valorConDescuento) }}</strong>
      </div>
      <img
        :src="producto.imagen"
        :alt="producto.descripcion"
        class="w-full h-full object-contain drop-shadow-2xl"
        loading="lazy"
      >
    </div>

    <div class="product-card-details">
      <p class="product-category">{{ producto.categoria }}</p>
      <h3>{{ producto.descripcion }}</h3>
      <p v-if="producto.descuento === 0" class="product-base-price">
        {{ formatoMoneda.format(producto.valor) }}
      </p>
      <button
        class="card-buy-button"
        type="button"
        @click="emit('agregar-al-carrito', producto)"
      >
        Comprar
      </button>
    </div>
  </article>
</template>
