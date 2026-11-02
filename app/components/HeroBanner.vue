<script setup>
defineProps({
  producto: {
    type: Object,
    required: true,
  },
})
</script>

<template>
  <section class="hero-stage" aria-labelledby="hero-title">
    <span class="hero-backdrop-word" aria-hidden="true">PRO</span>
    <img
      class="hero-banner-image"
      src="/iphone-18-pro-banner.png"
      alt="iPhone 18 Pro en un escenario cinematográfico"
      fetchpriority="high"
    >

    <div class="hero-copy">
      <span class="hero-eyebrow">Presentamos</span>
      <h1 id="hero-title">iPhone 18 Pro</h1>
      <p class="hero-tagline">Diseñado para<br class="mobile-break"> trascender.</p>
      <p class="hero-caption">{{ producto.descripcion }}</p>
      <a class="buy-button hero-buy-button" href="#catalogo">Explorar productos</a>
    </div>
    <span class="hero-note">Una experiencia extraordinaria, de principio a fin.</span>
  </section>
</template>
