<!-- src/components/Cart.vue -->
<template>
  <div class="cart-modal" v-if="show">
    <div class="cart-content">
      <h2>🛒 Your Cart</h2>
      <ul v-if="cartItems.length">
        <li v-for="(item, index) in cartItems" :key="index">
          {{ item.name }} - {{ item.price }}
          <button class="remove-btn" @click="$emit('removeFromCart', index)">Remove ❌</button>
        </li>
      </ul>
      <p v-else>Your cart is empty.</p>
      <button class="close-cart-btn" @click="$emit('closeCart')">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['cartItems', 'show'],
  emits: ['closeCart', 'removeFromCart']
}
</script>

<style scoped>
/* Styling seperti sebelumnya */
</style>
