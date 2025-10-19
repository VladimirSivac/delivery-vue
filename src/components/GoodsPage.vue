<script setup>
import { inject, computed, ref } from 'vue'
import { useRoute } from 'vue-router' // <-- Импортируем useRoute
import Header from './Header.vue'
import Footer from './Footer.vue'
import DishCard from './DishCard.vue'

// 1. Получаем данные и методы
const { dishes, restaurants } = inject('data')
const { addToCart } = inject('cartData') // Предполагаем, что вам нужна эта функция

// Получаем текущий маршрут
const route = useRoute()

// Получаем ID ресторана из URL (параметр :id)
const currentRestaurantId = route.params.id

// 2. Вычисляем (computed) название текущего ресторана
const currentRestaurant = computed(() => {
  // Находим объект ресторана по ID. ID из URL - это строка, поэтому используем ==
  const id = Number(currentRestaurantId)
  return restaurants.value.find((r) => r.id === id)
})

// Вычисляем заголовок для отображения
const restaurantTitle = computed(() => {
  return currentRestaurant.value ? currentRestaurant.value.title : 'Ресторан не найден'
})

// Вычисляем блюда, относящиеся к этому ресторану
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
