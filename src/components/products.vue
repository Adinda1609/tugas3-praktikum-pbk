<template>
  <section id="products" class="products-section">
    <div class="container">
      <h2 class="section-title">Our Lovely Collection 💕</h2>
      <div class="products-grid">
        <div 
          class="product-card" 
          v-for="product in products" 
          :key="product.id"
          @click="$emit('addToCart', product)"
        >
          <div class="card-image">
            <img :src="product.image" :alt="product.name" class="product-image" />
            <div class="card-badge">{{ product.badge }}</div>
          </div>
          <div class="card-content">
            <h3>{{ product.name }}</h3>
            <p class="product-description">{{ product.description }}</p>
            <div class="price-section">
              <span class="price">{{ product.price }}</span>
              <span class="old-price" v-if="product.oldPrice">{{ product.oldPrice }}</span>
            </div>
            <button class="add-to-cart-btn">Add to Cart 🛒</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: ['products'],
  emits: ['addToCart']
}
</script>
