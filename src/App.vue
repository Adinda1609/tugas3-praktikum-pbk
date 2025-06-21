<template>
  <div id="app">
    <!-- Navbar -->
    <Navbar 
      :isMenuOpen="isMenuOpen" 
      :cartCount="cartItems.length"
      @toggleMenu="toggleMenu"
      @closeMenu="closeMenu"
      @openCart="toggleCart"
    />

    <!-- Carousel -->
    <Carousel 
      :slides="heroSlides" 
      :currentSlide="currentSlide"
      @goToSlide="goToSlide"
    />

    <!-- Products -->
    <Products 
      :products="products"
      @addToCart="addToCart"
    />

    <!-- About -->
    <About />

    <!-- Footer -->
    <Footer />

    <!-- Cart Modal -->
    <Cart 
      :cartItems="cartItems"
      :show="showCart"
      @closeCart="toggleCart"
      @removeFromCart="removeFromCart"
    />

    <!-- Notification -->
    <div class="notification" :class="{ show: showNotification }">
      {{ notificationMessage }}
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Carousel from './components/Carousel.vue'
import Products from './components/Products.vue'
import About from './components/About.vue'
import Footer from './components/Footer.vue'
import Cart from './components/Cart.vue'

export default {
  name: 'App',
  components: {
    Navbar,
    Carousel,
    Products,
    About,
    Footer,
    Cart
  },
  data() {
    return {
      isMenuOpen: false,
      currentSlide: 0,
      cartItems: [],
      showCart: false,
      showNotification: false,
      notificationMessage: '',
      heroSlides: [
        {
          title: "Welcome to Bucket Mart 🌸",
          description: "Discover our dreamy collection of carefully curated treasures that bring joy to your everyday life.",
          emoji: "🛍️💕"
        },
        {
          title: "New Arrivals ✨",
          description: "Fresh picks just landed! Explore our latest collection of vintage-inspired goodies.",
          emoji: "🌺🎀"
        },
        {
          title: "Special Offers 💖",
          description: "Sweet deals await! Enjoy up to 30% off on selected items this week only.",
          emoji: "🎁💫"
        }
      ],
      products: [
        {
          id: 1,
          name: "Vintage Rose Bucket",
          description: "Adorable vintage-style bucket perfect for organizing your treasures",
          price: "$24.99",
          oldPrice: "$34.99",
          badge: "Sale!",
          image: new URL('./assets/product1.jpeg', import.meta.url).href
        },
        {
          id: 2,
          name: "Pearl Handle Basket",
          description: "Elegant basket with pearl-like handles for your shopping adventures",
          price: "$32.50",
          badge: "New",
          image: new URL('./assets/product2.jpg', import.meta.url).href
        },
        {
          id: 3,
          name: "Floral Storage Set",
          description: "Set of 3 beautiful floral storage containers for your room",
          price: "$45.00",
          oldPrice: "$55.00",
          badge: "Popular",
          image: new URL('./assets/product3.jpg', import.meta.url).href
        },
        {
          id: 4,
          name: "Lace Trim Organizer",
          description: "Cotton organizer with delicate lace trim details",
          price: "$28.75",
          badge: "Trending",
          image: new URL('./assets/product4.jpg', import.meta.url).href
        },
        {
          id: 5,
          name: "Shabby Chic Bucket",
          description: "Distressed finish bucket with vintage charm",
          price: "$36.99",
          badge: "Limited",
          image: new URL('./assets/product5.webp', import.meta.url).href
        },
        {
          id: 6,
          name: "Ribbon Storage Box",
          description: "Pretty storage box adorned with satin ribbons",
          price: "$22.50",
          oldPrice: "$29.99",
          badge: "Sale!",
          image: new URL('./assets/product6.jpg', import.meta.url).href
        }
      ]
    }
  },
  mounted() {
    this.startCarousel();
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
    startCarousel() {
      setInterval(() => {
        this.nextSlide();
      }, 4000);
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
      setTimeout(() => {
        this.showNotification = false;
      }, 3000);
    }
  }
}
</script>

<style src="./style.css"></style>
