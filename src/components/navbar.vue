<template>
  <nav class="navbar">
    <div class="nav-container">
      <div class="nav-brand">
        <h2>🌸 Bucket Mart</h2>
      </div>
      <ul class="nav-menu" :class="{ active: isMenuOpen }">
        <li><a href="#home" @click="closeMenu">Home</a></li>
        <li><a href="#products" @click="closeMenu">Products</a></li>
        <li><a href="#about" @click="closeMenu">About</a></li>
        <li><a href="#contact" @click="closeMenu">Contact</a></li>
        <li>
          <a href="#" class="nav-cart" @click.prevent="openCart">
            🛍️ Cart ({{ cartCount }})
          </a>
        </li>
      </ul>
      <div class="hamburger" :class="{ active: isMenuOpen }" @click="toggleMenu">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  props: ['isMenuOpen', 'cartCount'],
  emits: ['toggleMenu', 'closeMenu', 'openCart'],
  methods: {
    toggleMenu() {
      this.$emit('toggleMenu');
    },
    closeMenu() {
      this.$emit('closeMenu');
    },
    openCart() {
      this.$emit('closeMenu');
      this.$emit('openCart');
    }
  }
}
</script>
