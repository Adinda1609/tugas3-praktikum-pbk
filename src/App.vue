<template>
  <div id="app">
    <Navbar 
      :isMenuOpen="isMenuOpen" 
      :cartCount="cartItems.length"
      @toggleMenu="toggleMenu"
      @closeMenu="closeMenu"
      @openCart="toggleCart"
    />

    <Carousel 
      :slides="heroSlides" 
      :currentSlide="currentSlide"
      @goToSlide="goToSlide"
    />

    <Products 
      :products="products"
      @addToCart="addToCart"
    />

    <About />

    <Footer />

    <Cart 
      :cartItems="cartItems"
      :show="showCart"
      @closeCart="toggleCart"
      @removeFromCart="removeFromCart"
    />

    <div class="notification" :class="{ show: showNotification }">
      {{ notificationMessage }}
    </div>
  </div>
</template>

<script>
import Navbar from './components/navbar.vue'
import Carousel from './components/carousel.vue'
import Products from './components/products.vue'
import About from './components/about.vue'
import Footer from './components/footer.vue'
import Cart from './components/cart.vue'

export default {
  components: { Navbar, Carousel, Products, About, Footer, Cart },
  data() {
    return {
      isMenuOpen: false,
      currentSlide: 0,
      cartItems: [],
      showCart: false,
      showNotification: false,
      notificationMessage: '',
      heroSlides: [
        { title: "Welcome to Bucket Mart 🌸", description: "Discover dreamy collections.", emoji: "🛍️💕" },
        { title: "New Arrivals ✨", description: "Explore our latest goodies.", emoji: "🌺🎀" },
        { title: "Special Offers 💖", description: "Up to 30% off this week!", emoji: "🎁💫" }
      ],
      products: [
        { id: 1, name: "Vintage Rose Bucket", description: "Adorable vintage-style bucket", price: "$24.99", oldPrice: "$34.99", badge: "Sale!", image: new URL('./assets/product1.jpeg', import.meta.url).href },
        { id: 2, name: "Pearl Handle Basket", description: "Elegant basket with pearl handles", price: "$32.50", badge: "New", image: new URL('./assets/product2.webp', import.meta.url).href },
        { id: 3, name: "Lilac Whisper", description: "Set of 3 floral containers", price: "$45.00", oldPrice: "$55.00", badge: "Popular", image: new URL('./assets/product3.webp', import.meta.url).href },
        { id: 4, name: "Love Buddy", description: "Cotton organizer with lace", price: "$28.75", badge: "Trending", image: new URL('./assets/product4.jpg', import.meta.url).href },
        { id: 5, name: "Shabby Chic Bucket", description: "Distressed finish bucket", price: "$36.99", badge: "Limited", image: new URL('./assets/product5.webp', import.meta.url).href },
        { id: 6, name: "Luxe Bouqet", description: "Box adorned with satin ribbons", price: "$22.50", oldPrice: "$29.99", badge: "Sale!", image: new URL('./assets/product6.jpg', import.meta.url).href }
      ]
    }
  },
  mounted() {
    setInterval(this.nextSlide, 4000);
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    closeMenu() {
      this.isMenuOpen = false;
    },
    toggleCart() {
      this.showCart = !this.showCart;
    },
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.heroSlides.length;
    },
    goToSlide(index) {
      this.currentSlide = index;
    },
    addToCart(product) {
      this.cartItems.push(product);
      this.showNotificationMsg(`${product.name} added to cart! 💕`);
    },
    removeFromCart(index) {
      this.cartItems.splice(index, 1);
    },
    showNotificationMsg(message) {
      this.notificationMessage = message;
      this.showNotification = true;
      setTimeout(() => this.showNotification = false, 3000);
    }
  }
}
</script>

<style src="./style.css"></style>
