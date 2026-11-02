<script setup>
defineProps({
  items: {
    type: Array,
    required: true,
  },
  subtotal: {
    type: Number,
    required: true,
  },
  descuentos: {
    type: Number,
    required: true,
  },
  total: {
    type: Number,
    required: true,
  },
})

const emit = defineEmits([
  'incrementar',
  'decrementar',
  'eliminar',
  'finalizar-compra',
  'cerrar',
])

const formatoMoneda = new Intl.NumberFormat('es-CO', {
  style: 'currency',
  currency: 'COP',
  maximumFractionDigits: 0,
})
</script>

<template>
  <div class="cart-overlay" @click.self="emit('cerrar')">
    <aside class="cart-drawer" role="dialog" aria-modal="true" aria-labelledby="cart-title">
      <div class="cart-heading">
        <div>
          <p class="section-kicker">Tu selección</p>
          <h2 id="cart-title">Tu bolsa</h2>
        </div>
        <button class="cart-close" aria-label="Cerrar carrito" @click="emit('cerrar')">×</button>
      </div>

      <div v-if="items.length" class="cart-content">
        <div class="cart-table-wrap">
          <table class="cart-table">
            <thead>
              <tr>
                <th scope="col">Producto</th>
                <th scope="col">Valor unitario</th>
                <th scope="col">Cantidad</th>
                <th scope="col">Subtotal</th>
                <th scope="col"><span class="sr-only">Acciones</span></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in items" :key="item.producto.id">
                <td>
                  <div class="cart-product">
                    <img :src="item.producto.imagen" :alt="item.producto.descripcion">
                    <div>
                      <strong>{{ item.producto.descripcion }}</strong>
                      <span v-if="item.producto.descuento > 0">
                        Descuento: {{ item.producto.descuento }}%
                      </span>
                    </div>
                  </div>
                </td>
                <td>
                  <span
                    v-if="item.producto.descuento > 0"
                    class="original-price"
                  >
                    {{ formatoMoneda.format(item.valorUnitario) }}
                  </span>
                  <span class="discounted-price">
                    {{ formatoMoneda.format(item.valorConDescuento) }}
                  </span>
                </td>
                <td>
                  <div class="quantity-control">
                    <button
                      :aria-label="`Disminuir cantidad de ${item.producto.descripcion}`"
                      @click="emit('decrementar', item.producto.id)"
                    >
                      −
                    </button>
                    <span>{{ item.cantidad }}</span>
                    <button
                      :aria-label="`Aumentar cantidad de ${item.producto.descripcion}`"
                      @click="emit('incrementar', item.producto.id)"
                    >
                      +
                    </button>
                  </div>
                </td>
                <td class="line-total">{{ formatoMoneda.format(item.subtotal) }}</td>
                <td>
                  <button
                    class="remove-item-button"
                    :aria-label="`Eliminar ${item.producto.descripcion} del carrito`"
                    @click="emit('eliminar', item.producto.id)"
                  >
                    Eliminar
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="cart-summary">
          <p><span>Subtotal</span><strong>{{ formatoMoneda.format(subtotal) }}</strong></p>
          <p><span>Descuentos</span><strong>-{{ formatoMoneda.format(descuentos) }}</strong></p>
          <p class="cart-total"><span>Total</span><strong>{{ formatoMoneda.format(total) }}</strong></p>
          <span class="cart-tax-note">El IVA del 19% se detalla en la factura.</span>
          <button
            class="checkout-button"
            :disabled="items.length === 0"
            @click="emit('finalizar-compra')"
          >
            Finalizar compra
          </button>
        </div>
      </div>

      <div v-else class="cart-empty">
        <span class="empty-bag-icon" aria-hidden="true">⌑</span>
        <h3>Tu bolsa está esperando.</h3>
        <p>Descubre algo extraordinario para ti.</p>
        <button class="buy-button" @click="emit('cerrar')">Seguir explorando</button>
        <button class="checkout-button" disabled>Finalizar compra</button>
      </div>
    </aside>
  </div>
</template>
