<script setup>
import { inject, computed } from 'vue'
import CartItem from './CartItem.vue'

const { cart, totalCartPrice, closeModal } = inject('cartData')

const isCartEmpty = computed(() => cart.value.length === 0)

const createOrder = () => {
  alert(`Оформляем заказ на сумму ${totalCartPrice.value} ₽`)
  // Здесь должна быть логика очистки корзины и отправки данных на сервер
}
</script>

<template>
  <div class="card-modal__overlay open" @click.self="closeModal">
    <div class="cart-modal">
      <div class="card-modal__header">
        <h2 class="card-modal__header--title">Корзина</h2>
        <span class="card-modal__header--close" @click="closeModal">
          <img src="/icons/close.svg" alt="Close" />
        </span>
      </div>

      <div v-if="!isCartEmpty">
        <div class="card-modal__body">
          <CartItem v-for="item in cart" :key="item.id" :item="item" />
        </div>

        <div class="card-modal__footer">
          <div class="card-modal__footer--price">{{ totalCartPrice }} ₽</div>
          <div class="card-modal__footer--controls">
            <button class="btn btn-primary" @click="createOrder">Оформить заказ</button>
            <button class="btn btn-outline" @click="closeModal">Отмена</button>
          </div>
        </div>
      </div>

      <div v-else class="card-modal__body text-center">
        <p class="card-modal__header--title">Корзина пуста</p>
        <button class="btn btn-primary mt-4" @click="closeModal">К покупкам!</button>
      </div>
    </div>
  </div>
</template>
