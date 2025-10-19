<script setup>
import { inject } from 'vue'
import { RouterLink } from 'vue-router'

const { openModal } = inject('cartData')
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="header-box">
        <router-link to="/" class="logo header-logo">
          <img src="/logo.png" alt="Header-logo" />
        </router-link>
        <div class="header-controls">
          <button class="btn btn-primary">
            <img src="/icons/user.svg" alt="User-logo" />
            Войти
          </button>
          <button class="btn btn-outline" @click="openModal">
            <img src="/icons/shopping-cart.svg" alt="Shopping-cart-logo" />
            Корзина
          </button>
        </div>
      </div>
    </div>
  </header>
</template>
