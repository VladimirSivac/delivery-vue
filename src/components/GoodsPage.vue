<script setup>
import { inject, computed, ref } from 'vue'
import { useRoute } from 'vue-router'
import Header from './Header.vue'
import Footer from './Footer.vue'
import DishCard from './DishCard.vue'

const { dishes, restaurants } = inject('data')
const { addToCart } = inject('cartData')

const route = useRoute()

const currentRestaurantId = route.params.id

const currentRestaurant = computed(() => {
  const id = Number(currentRestaurantId)
  return restaurants.value.find((r) => r.id === id)
})

const restaurantTitle = computed(() => {
  return currentRestaurant.value ? currentRestaurant.value.title : 'Ресторан не найден'
})

const currentRestaurantDishes = computed(() => {
  const id = Number(currentRestaurantId)
  return dishes.value.filter((dish) => dish.restaurantId === id)
})
</script>

<template>
  <Header />
  <main class="main">
    <section class="products">
      <div class="container">
        <h1 class="products-header-title">{{ restaurantTitle }} - Меню</h1>

        <div v-if="currentRestaurantDishes.length > 0" class="products-wrapper">
          <DishCard
            v-for="dish in currentRestaurantDishes"
            :key="dish.id"
            :dish="dish"
            @add-to-cart="addToCart"
          />
        </div>
        <div v-else>
          <p>Блюда для этого ресторана пока отсутствуют.</p>
        </div>
      </div>
    </section>
  </main>
  <Footer />
</template>
