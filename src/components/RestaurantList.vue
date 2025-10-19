<script setup>
import { ref, computed } from 'vue'
import RestaurantCard from './RestaurantCard.vue'

// 1. ПОЛНЫЙ СПИСОК РЕСТОРАНОВ (с исправленными путями)
const mockRestaurants = [
  {
    id: 1,
    title: 'Пицца плюс',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Пицца',
    imageUrl: '/rests/rest-1.jpg',
  },
  {
    id: 2,
    title: 'Тануки',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Суши',
    imageUrl: '/rests/rest-2.jpg',
  },
  {
    id: 3,
    title: 'FoodBand',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Пицца',
    imageUrl: '/rests/rest-3.jpg',
  },
  {
    id: 4,
    title: 'Жадина-пицца',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Пицца',
    imageUrl: '/rests/rest-4.jpg',
  },
  {
    id: 5,
    title: 'Точка еды',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Бургеры',
    imageUrl: '/rests/rest-5.jpg',
  },
  {
    id: 6,
    title: 'PizzaBurger',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Пицца',
    imageUrl: '/rests/rest-6.jpg',
  },
]

// Состояние для поиска
const restaurants = ref(mockRestaurants)
const searchQuery = ref('')

// Отфильтрованный список (computed)
const filteredRestaurants = computed(() => {
  const query = searchQuery.value.toLowerCase().trim()
  if (!query) return restaurants.value

  return restaurants.value.filter((rest) => rest.title.toLowerCase().includes(query))
})
</script>

<template>
  <section class="products">
    <div class="container">
      <div class="products-header">
        <h2 class="products-header-title">Рестораны</h2>
        <input
          type="text"
          class="products-header-search"
          placeholder="Поиск блюд и ресторанов"
          v-model="searchQuery"
        />
      </div>
      <div class="products-wrapper" id="rests-container">
        <RestaurantCard v-for="rest in filteredRestaurants" :key="rest.id" :restaurant="rest" />
      </div>
    </div>
  </section>
</template>
