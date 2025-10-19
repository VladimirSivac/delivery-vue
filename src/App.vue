<script setup>
import { ref, computed, provide, watch, onMounted } from 'vue'
import MainPage from './components/MainPage.vue'
import ModalPage from './components/ModalPage.vue'

const dishes = ref([
  {
    id: 1,
    name: 'Ролл угорь стандарт',
    price: 250,
    description: 'Рис, угорь, соус унаги, кунжут, водоросли нори.',
    imageUrl: '/goods/good-1.jpg',
    restaurantId: 1,
  },
  {
    id: 2,
    name: 'Ролл лосось',
    price: 395,
    description: 'Рис, лосось, сливочный сыр, нори.',
    imageUrl: '/goods/good-2.jpg',
    restaurantId: 1,
  },

  {
    id: 3,
    name: 'Сет Филадельфия',
    price: 1200,
    description: 'Разнообразный сет с лососем и авокадо.',
    imageUrl: '/goods/good-3.jpg',
    restaurantId: 2,
  },
  {
    id: 4,
    name: 'Пицца Пепперони',
    price: 900,
    description: 'Острая пепперони, сыр моцарелла, томатный соус.',
    imageUrl: '/goods/good-4.jpg',
    restaurantId: 3,
  },
  {
    id: 5,
    name: 'Бургер классический',
    price: 450,
    description: 'Котлета, свежие овощи, соус, булочка.',
    imageUrl: '/goods/good-5.jpg',
    restaurantId: 4,
  },
  {
    id: 6,
    name: 'Лапша WOK',
    price: 350,
    description: 'Пшеничная лапша с курицей и овощами.',
    imageUrl: '/goods/good-6.jpg',
    restaurantId: 5,
  },
])

const restaurants = ref([
  {
    id: 1,
    title: 'Пицца плюс',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Пицца',
    imageUrl: '../assets/images/rests/rest-1.jpg',
  },
  {
    id: 2,
    title: 'Тануки',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Суши',
    imageUrl: '../assets/images/rests/rest-2.jpg',
  },
  {
    id: 3,
    title: 'FoodBand',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Пицца',
    imageUrl: '../assets/images/rests/rest-3.jpg',
  },
  {
    id: 4,
    title: 'Жадина-пицца',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Пицца',
    imageUrl: '../assets/images/rests/rest-4.jpg',
  },
  {
    id: 5,
    title: 'Точка еды',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Бургеры',
    imageUrl: '../assets/images/rests/rest-5.jpg',
  },
  {
    id: 6,
    title: 'PizzaBurger',
    time: 50,
    rating: 4.5,
    price: 900,
    group: 'Пицца',
    imageUrl: '../assets/images/rests/rest-6.jpg',
  },
])

// --- Cart Logic ---
const cart = ref([])
const isModalOpen = ref(false)

const totalCartPrice = computed(() =>
  cart.value.reduce((acc, item) => acc + item.price * item.count, 0),
)

const openModal = () => {
  isModalOpen.value = true
}
const closeModal = () => {
  isModalOpen.value = false
}

const addToCart = (dish) => {
  const existingItem = cart.value.find((item) => item.id === dish.id)
  if (existingItem) {
    existingItem.count++
  } else {
    cart.value.push({ ...dish, count: 1 })
  }
}

const changeItemCount = (dishId, delta) => {
  const item = cart.value.find((item) => item.id === dishId)
  if (item) {
    item.count += delta
    if (item.count <= 0) {
      removeFromCart(dishId)
    }
  }
}

const removeFromCart = (dishId) => {
  cart.value = cart.value.filter((item) => item.id !== dishId)
}

onMounted(() => {
  const savedCart = localStorage.getItem('deliveryFoodCart')
  if (savedCart) {
    cart.value = JSON.parse(savedCart)
  }
})

watch(
  cart,
  (newCart) => {
    localStorage.setItem('deliveryFoodCart', JSON.stringify(newCart))
  },
  { deep: true },
)

provide('cartData', {
  cart,
  totalCartPrice,
  openModal,
  closeModal,
  addToCart,
  removeFromCart,
  changeItemCount,
})
provide('data', {
  restaurants,
  dishes,
})
</script>

<template>
  <div class="page-wrapper">
    <RouterView />
    <ModalPage v-if="isModalOpen" />
  </div>
</template>
