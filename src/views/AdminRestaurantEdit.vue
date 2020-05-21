<template>
  <div class="container py-5">
    <AdminRestaurantForm :initial-restaurant="restaurant" @after-submit="handleAfterSubmit" />
  </div>
</template>

<script>
import AdminRestaurantForm from "./../components/AdminRestaurantForm.vue";

const dummyData = {
  restaurant: {
    id: 12,
    name: "Oliver Padberg",
    tel: "865-523-0270 x58016",
    address: "771 Oberbrunner Hollow",
    opening_hours: "08:00",
    description:
      "Magni qui facilis asperiores. Voluptatem cumque corrupti ea at voluptatem. Assumenda esse esse fuga autem dolor qui. Veniam qui eius vero magnam ut inventore magni est.",
    image:
      "https://loremflickr.com/320/240/restaurant,food/?random=22.348939427568215",
    viewCounts: 5,
    createdAt: "2020-02-28T14:38:32.000Z",
    updatedAt: "2020-04-10T10:48:16.000Z",
    CategoryId: 1,
    Category: {
      id: 1,
      name: "中式料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-05-17T03:45:22.000Z"
    }
  }
};

export default {
  components: {
    AdminRestaurantForm
  },
  methods: {
    handleAfterSubmit(formData) {
      // 透過 API 將表單資料送到伺服器
      for (let [name, value] of formData.entries()) {
        console.log(name + ": " + value);
      }
    },
    fetchRestaurant(restaurantId) {
      console.log("fetchRestaurant id:", restaurantId);
      const { restaurant } = dummyData;
      this.restaurant = {
        ...this.restaurant,
        id: restaurant.id,
        name: restaurant.name,
        categoryId: restaurant.CategoryId,
        tel: restaurant.tel,
        address: restaurant.address,
        description: restaurant.description,
        image: restaurant.image,
        openingHours: restaurant.opening_hours
      };
    }
  },
  data() {
    return {
      restaurant: {
        id: -1,
        name: "",
        categoryId: "",
        tel: "",
        address: "",
        description: "",
        image: "",
        openingHours: ""
      }
    };
  },
  created() {
    const { id } = this.$route.params;
    this.fetchRestaurant(id);
  }
};
</script>