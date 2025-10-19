<script setup>
import { inject } from 'vue'

const { changeItemCount, removeFromCart } = inject('cartData')

const props = defineProps({
  item: {
    type: Object, // Ожидаем { id, name, price, count }
    required: true,
  },
})

const increaseCount = () => changeItemCount(props.item.id, 1)
const decreaseCount = () => changeItemCount(props.item.id, -1)
</script>

<template>
  <div class="card-item">
    <p class="card-item__title">{{ item.name }}</p>
    <div class="card-item__controls">
      <div class="card-item__controls--price">{{ item.price * item.count }} ₽</div>
      <button class="btn btn-outline" @click="decreaseCount">-</button>
      <div class="card-item__controls--count">{{ item.count }}</div>
      <button class="btn btn-outline" @click="increaseCount">+</button>
    </div>
    <span class="card-modal__header--close" @click="removeFromCart(item.id)">
      <img src="/icons/close.svg" alt="Remove" class="w-4 h-4" />
    </span>
  </div>
</template>
