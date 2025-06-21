<template>
  <section id="home" class="hero-section">
    <div class="carousel-container">
      <div class="carousel-wrapper" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
        <div class="carousel-slide" v-for="(slide, index) in slides" :key="index">
          <div class="slide-content">
            <div class="slide-text">
              <h1>{{ slide.title }}</h1>
              <p>{{ slide.description }}</p>
              <button class="cta-button" @click="shopNow">Shop Now ✨</button>
            </div>
            <div class="slide-image">
              <div class="image-placeholder">{{ slide.emoji }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="carousel-dots">
        <span 
          v-for="(slide, index) in slides" 
          :key="index" 
          class="dot"
          :class="{ active: currentSlide === index }"
          @click="$emit('goToSlide', index)"
        ></span>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: ['slides', 'currentSlide'],
  emits: ['goToSlide'],
  methods: {
    shopNow() {
      document.getElementById('products').scrollIntoView({ behavior: 'smooth' });
    }
  }
}
</script>
