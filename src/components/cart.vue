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
.cart-modal {
  position: fixed;
  top: 0; left: 0;
  width: 100vw; height: 100vh;
  background: rgba(0, 0, 0, 0.3);
  display: flex; justify-content: center; align-items: center;
  z-index: 9999;
}
.cart-content {
  background: linear-gradient(135deg, #fffafa, #fce7ec);
  padding: 2rem; border-radius: 20px;
  width: 90%; max-width: 500px;
  box-shadow: 0 10px 30px rgba(218, 165, 180, 0.3);
  text-align: center; animation: popUp 0.3s ease;
}
.cart-content h2 { color: #5d4e75; margin-bottom: 1.5rem; }
.cart-content ul { list-style: none; padding: 0; max-height: 300px; overflow-y: auto; margin-bottom: 1rem; }
.cart-content li {
  background: #fff; margin-bottom: 0.5rem;
  padding: 0.7rem 1rem; border-radius: 12px;
  display: flex; justify-content: space-between; align-items: center;
  color: #7a6b83; font-weight: 500;
}
.remove-btn {
  background: none; border: none;
  color: #d9534f; cursor: pointer;
  font-size: 0.9rem; font-weight: bold;
}
.close-cart-btn {
  background: linear-gradient(45deg, #dab4b4, #c49a9a);
  color: white; padding: 12px 30px;
  border: none; border-radius: 30px;
  font-weight: bold; cursor: pointer;
  transition: 0.3s ease; font-size: 1rem;
  box-shadow: 0 6px 20px rgba(196, 154, 154, 0.3);
}
.close-cart-btn:hover {
  background: linear-gradient(45deg, #c49a9a, #a88080);
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(196, 154, 154, 0.5);
}
@keyframes popUp {
  0% { transform: scale(0.9); opacity: 0; }
  100% { transform: scale(1); opacity: 1; }
}
</style>
