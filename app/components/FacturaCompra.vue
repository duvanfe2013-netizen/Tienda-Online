<script setup>
import { computed } from 'vue'

const props = defineProps({
  items: {
    type: Array,
    required: true,
  },
  numeroFactura: {
    type: String,
    required: true,
  },
  fecha: {
    type: String,
    required: true,
  },
})

const emit = defineEmits(['nueva-compra'])

const formatoMoneda = new Intl.NumberFormat('es-CO', {
  style: 'currency',
  currency: 'COP',
  maximumFractionDigits: 0,
})

const subtotal = computed(() => props.items.reduce(
  (total, item) => total + item.valorUnitario * item.cantidad,
  0,
))

const subtotalConDescuento = computed(() => props.items.reduce(
  (total, item) => total + item.subtotal,
  0,
))

const totalDescuentos = computed(() => props.items.reduce(
  (total, item) => total + item.descuentoUnitario * item.cantidad,
  0,
))

const iva = computed(() => Math.round(subtotalConDescuento.value * 0.19))
const totalPagar = computed(() => subtotalConDescuento.value + iva.value)
</script>

<template>
  <div class="modal-backdrop receipt-backdrop">
    <section class="receipt-modal invoice-modal" role="dialog" aria-modal="true" aria-labelledby="invoice-title">
      <div class="receipt-success-mark" aria-hidden="true">✓</div>
      <p class="section-kicker">Factura de compra</p>
      <h2 id="invoice-title">Gracias por tu compra.</h2>
      <div class="receipt-order-meta">
        <div>
          <span>Número consecutivo</span>
          <strong>{{ numeroFactura }}</strong>
        </div>
        <div>
          <span>Fecha</span>
          <strong>{{ fecha }}</strong>
        </div>
      </div>

      <div class="invoice-table-wrap">
        <table class="invoice-table">
          <thead>
            <tr>
              <th scope="col">Descripción</th>
              <th scope="col">Cantidad</th>
              <th scope="col">Valor unitario</th>
              <th scope="col">Descuento</th>
              <th scope="col">Valor con descuento</th>
              <th scope="col">Subtotal</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in items" :key="item.producto.id">
              <td>
                <div class="invoice-product">
                  <img :src="item.producto.imagen" :alt="item.producto.descripcion">
                  <span>{{ item.producto.descripcion }}</span>
                </div>
              </td>
              <td>{{ item.cantidad }}</td>
              <td>{{ formatoMoneda.format(item.valorUnitario) }}</td>
              <td>
                {{ item.producto.descuento }}%
                <span v-if="item.descuentoUnitario">
                  (−{{ formatoMoneda.format(item.descuentoUnitario * item.cantidad) }})
                </span>
              </td>
              <td>{{ formatoMoneda.format(item.valorConDescuento) }}</td>
              <td>{{ formatoMoneda.format(item.subtotal) }}</td>
            </tr>
          </tbody>
        </table>
      </div>

      <dl class="invoice-totals">
        <div>
          <dt>Subtotal</dt>
          <dd>{{ formatoMoneda.format(subtotal) }}</dd>
        </div>
        <div>
          <dt>Total de descuentos</dt>
          <dd>−{{ formatoMoneda.format(totalDescuentos) }}</dd>
        </div>
        <div>
          <dt>Subtotal después de descuentos</dt>
          <dd>{{ formatoMoneda.format(subtotalConDescuento) }}</dd>
        </div>
        <div>
          <dt>IVA (19%)</dt>
          <dd>{{ formatoMoneda.format(iva) }}</dd>
        </div>
        <div class="invoice-grand-total">
          <dt>Total a pagar</dt>
          <dd>{{ formatoMoneda.format(totalPagar) }}</dd>
        </div>
      </dl>

      <button class="checkout-button receipt-finish-button" @click="emit('nueva-compra')">
        Nueva compra
      </button>
    </section>
  </div>
</template>
