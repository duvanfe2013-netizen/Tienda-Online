<script setup>
defineProps({
  nombreTienda: {
    type: String,
    required: true,
  },
  anio: {
    type: Number,
    required: true,
  },
  contacto: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <footer class="store-footer">
    <span class="footer-mark" aria-hidden="true">●</span>
    <p>Diseñado para quienes buscan lo extraordinario.</p>
    <span>{{ nombreTienda }} · {{ anio }} · {{ contacto }}</span>
  </footer>
</template>
