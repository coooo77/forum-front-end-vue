<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">人氣餐廳</h1>
    <topRestaurant
      v-for="restaurant in restaurants"
      :key="restaurant.id"
      :restaurant="restaurant"
      @after-add-favorite="afterAddFavorite"
      @after-delete-favorite="afterDeleteFavorite"
    />
    <hr />
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";
import topRestaurant from "./../components/topRestaurant";
import RestaurantsAPI from "../apis/restaurants";
import { Toast } from "../utils/helpers";
export default {
  components: {
    NavTabs,
    topRestaurant
  },
  data() {
    return {
      restaurants: []
    };
  },
  methods: {
    async fetchTopRestaurants() {
      try {
        const response = await RestaurantsAPI.getTopRestaurants();
        if (response.statusText !== "OK") {
          throw new Error(response.statusText);
        }
        const { restaurants } = response.data;
        this.restaurants = restaurants;
      } catch (error) {
        console.log("error", error);
        Toast.fire({
          icon: "error",
          title: "無法取得人氣餐廳資料，請稍後再試"
        });
      }
    },
    async afterAddFavorite(playload) {
      const indexOfPlayLoad = this.restaurants
        .map(restaurant => restaurant.id)
        .indexOf(playload.id);
      this.restaurants.splice(indexOfPlayLoad, 1, playload);
    },
    afterDeleteFavorite(playload) {
      const indexOfPlayLoad = this.restaurants
        .map(restaurant => restaurant.id)
        .indexOf(playload.id);
      this.restaurants.splice(indexOfPlayLoad, 1, playload);
    }
  },
  created() {
    this.fetchTopRestaurants();
  }
};
</script>