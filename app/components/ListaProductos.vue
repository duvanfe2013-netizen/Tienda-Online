<script setup>
import ProductoCard from './ProductoCard.vue'

defineProps({
  productos: {
    type: Array,
    required: true,
  },
})

const emit = defineEmits(['agregar-producto'])
</script>

<template>
  <section id="catalogo" class="collection-section">
    <div class="section-heading">
      <div>
        <p class="section-kicker">La selección</p>
        <h2>Un mundo de posibilidades.</h2>
      </div>
      <p class="section-description">Tecnología que inspira.<br>Diseño que permanece.</p>
    </div>

    <div class="product-grid">
      <ProductoCard
        v-for="producto in productos"
        :key="producto.id"
        :producto="producto"
        @agregar-al-carrito="emit('agregar-producto', $event)"
      />
    </div>
  </section>
</template>
