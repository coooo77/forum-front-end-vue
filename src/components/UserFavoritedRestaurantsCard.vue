<template>
  <div class="card">
    <div class="card-header">
      <strong>{{FavoritedRestaurants.length}}</strong> 收藏的餐廳
    </div>
    <div class="card-body">
      <router-link
        v-for="favortiedRestaurant in FavoritedRestaurants"
        :key="favortiedRestaurant.id"
        :to="{ name:'restaurant', params:{id:favortiedRestaurant.id}}"
      >
        <img :src="favortiedRestaurant.image | emptyImage" width="60" height="60" class="avatar" />
      </router-link>
    </div>
  </div>
</template>

<script>
import { emptyImageFilter } from "./../utils/mixins";
export default {
  mixins: [emptyImageFilter],
  props: {
    FavoritedRestaurants: {
      type: Array,
      required: true
    }
  }
};
</script>