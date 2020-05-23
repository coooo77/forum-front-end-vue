<template>
  <div class="card mb-3" style="max-width: 540px;margin: auto;">
    <div class="row no-gutters">
      <div class="col-md-4">
        <router-link :to="{ name: 'restaurant', params: { id: restaurant.id }}">
          <img class="card-img" :src="restaurant.image | emptyImage" />
        </router-link>
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{restaurant.name}}</h5>
          <span class="badge badge-secondary">收藏數：{{restaurant.FavoriteCount}}</span>
          <p class="card-text">{{restaurant.description}}</p>
          <router-link :to="{ name: 'restaurant', params: { id: restaurant.id }}">
            <div class="btn btn-primary mr-2">Show</div>
          </router-link>
          <button
            v-if="restaurant.isFavorited"
            type="button"
            class="btn btn-danger mr-2"
            @click.stop.prevent="deleteFavorite(restaurant.id)"
          >移除最愛</button>
          <button
            v-else
            type="button"
            class="btn btn-primary"
            @click.stop.prevent="addFavorite(restaurant.id)"
          >加到最愛</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { emptyImageFilter } from "./../utils/mixins";
import UserAPI from "../apis/users";
import { Toast } from "../utils/helpers";

export default {
  mixins: [emptyImageFilter],
  props: {
    restaurant: {
      type: Object,
      required: true
    }
  },
  methods: {
    async addFavorite(restaurantId) {
      try {
        const { data } = await UserAPI.addFavorite({ restaurantId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.$emit("after-add-favorite", {
          ...this.restaurant,
          isFavorited: true,
          FavoriteCount: ++this.restaurant.FavoriteCount
        });
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法新增最愛，請稍後嘗試"
        });
        console.log("error", error);
      }
    },
    async deleteFavorite(restaurantId) {
      try {
        const { data } = await UserAPI.deleteFavorite({ restaurantId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.$emit("after-delete-favorite", {
          ...this.restaurant,
          isFavorited: false,
          FavoriteCount: --this.restaurant.FavoriteCount
        });
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法移除最愛，請稍後嘗試"
        });
        console.log("error", error);
      }
    }
  }
};
</script>