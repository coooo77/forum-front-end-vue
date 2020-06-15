<template>
  <div class="container py-5">
    <!-- 後台導覽頁籤 AdminNav -->
    <AdminNav />

    <router-link to="/admin/restaurants/new" class="btn btn-primary mb-4">New Restaurant</router-link>

    <!-- 後台餐廳列表 AdminRestaurantsTable -->
    <AdminRestaurantsTable v-bind:restaurants="restaurants" @after-delete="deleteRestaurant" />
  </div>
</template>

<script>
import AdminNav from "./../components/AdminNav";
import AdminRestaurantsTable from "./../components/AdminRestaurantsTable";
import adminAPI from "../apis/admin";
import { Toast } from "../utils/helpers";

export default {
  components: {
    AdminNav,
    AdminRestaurantsTable
  },
  data() {
    return {
      restaurants: []
    };
  },
  created() {
    this.fetchRestaurants();
  },
  methods: {
    async fetchRestaurants() {
      try {
        const { data, status, statusText } = await adminAPI.restaurants.get();
        if (status !== 200) {
          throw new Error(statusText);
        }
        this.restaurants = data.restaurants;
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取得餐廳，請稍後再試"
        });
      }
    },
    async deleteRestaurant(restaurantId) {
      try {
        const { data } = await adminAPI.restaurants.delete(restaurantId);
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.restaurants = this.restaurants.filter(
          restaurant => restaurant.id !== restaurantId
        );
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法刪除餐廳，請稍後再試"
        });
      }
    }
  }
};
</script>