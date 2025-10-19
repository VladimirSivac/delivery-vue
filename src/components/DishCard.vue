<script setup>
import { inject } from 'vue'

const { addToCart } = inject('cartData')

const props = defineProps({
  dish: {
    type: Object,
    required: true,
  },
})

const handleAddToCart = () => {
  addToCart(props.dish)
}
</script>

<template>
  <div class="products-card">
    <div class="products-card__image">
      <img :src="dish.imageUrl" :alt="dish.name" />
    </div>
    <div class="products-card__description">
      <div class="products-card__description-row">
        <h4 class="products-card__description--name">{{ dish.name }}</h4>
      </div>
      <div class="products-card__description-row">
        <p class="products-card__description--text">
          {{ dish.description }}
        </p>
      </div>
      <div class="products-card__description-row">
        <div class="products-card__description--controls">
          <button class="btn btn-primary" @click="handleAddToCart">
            В корзину
            <img src="/icons/shopping-cart-white.svg" alt="Cart icon" />
          </button>
          <span class="products-card__description-controls--price"> {{ dish.price }} ₽ </span>
        </div>
      </div>
    </div>
  </div>
</template>
