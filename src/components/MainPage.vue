<script setup>
import Header from './Header.vue'
import Footer from './Footer.vue'
import RestaurantList from './RestaurantList.vue'
</script>

<template>
  <Header />
  <main class="main">
    <section class="banner">
      <div class="container">
        <div class="banner-item">
          <h1 class="banner-item-title">
            Онлайн-сервис <br />
            доставки еды на дом
          </h1>
          <p class="banner-item-subtitle">
            Блюда из любимого ресторана привезет курьер в перчатках, маске и с антисептиком
          </p>
        </div>
      </div>
    </section>
    <RestaurantList />
  </main>
  <Footer />
</template>
