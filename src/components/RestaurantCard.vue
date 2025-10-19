<script>
export default {
  props: {
    restaurant: {
      type: Object,
      required: true,
    },
  },
}
</script>

<template>
  <router-link :to="`/rest/${restaurant.id}`" class="products-card">
    <div class="products-card__image">
      <img :src="restaurant.imageUrl" :alt="restaurant.title" />
    </div>
    <div class="products-card__description">
      <div class="products-card__description-row">
        <h3 class="products-card__description--title">{{ restaurant.title }}</h3>
        <div class="products-card__description--badge">{{ restaurant.time }} минут</div>
      </div>
      <div class="products-card__description-row">
        <div class="products-card__description-info">
          <div class="products-card__description-info--rating">
            <img src="/icons/star.svg" alt="Rating" />
            {{ restaurant.rating }}
          </div>
          <div class="products-card__description-info--price">От {{ restaurant.price }} ₽</div>
          <div class="products-card__description-info--group">{{ restaurant.group }}</div>
        </div>
      </div>
    </div>
  </router-link>
</template>
