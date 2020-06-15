<template>
  <table class="table">
    <thead class="thead-dark">
      <tr>
        <th scope="col">#</th>
        <th scope="col">Category</th>
        <th scope="col">Name</th>
        <th scope="col" width="300">操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="restaurant in restaurants" :key="restaurant.id">
        <th scope="row">{{ restaurant.id }}</th>
        <td>{{ restaurant.Category ? restaurant.Category.name : '未分類' }}</td>
        <td>{{ restaurant.name }}</td>
        <td class="d-flex justify-content-between">
          <router-link
            :to="{name: 'admin-restaurant', params: {id: restaurant.id}}"
            class="btn btn-link"
          >Show</router-link>

          <router-link
            :to="{name:'admin-restaurant-edit', params:{id:restaurant.id}}"
            class="btn btn-link"
          >Edit</router-link>

          <button
            type="button"
            class="btn btn-link"
            @click.stop.prevent="deleteRestaurant(restaurant.id)"
          >Delete</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "AdminRestaurantsTable",
  props: {
    restaurants: {
      type: Array,
      required: true
    }
  },
  methods: {
    deleteRestaurant(restaurantId) {
      this.$emit("after-delete", restaurantId);
    }
  }
};
</script>