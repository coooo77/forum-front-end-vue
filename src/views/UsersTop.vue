<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">美食達人</h1>
    <hr />
    <div class="row text-center">
      <topUser v-for="user in users" :key="user.id" :user="user" />
    </div>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";
import topUser from "./../components/topUser";
import usersAPI from "../apis/users";
import { Toast } from "./../utils/helpers";

export default {
  components: {
    NavTabs,
    topUser
  },
  data() {
    return {
      users: []
    };
  },
  methods: {
    async fetchUsers() {
      try {
        const { data } = await usersAPI.getTopUsers();

        this.users = data.users.map(user => ({
          id: user.id,
          name: user.name,
          image: user.image,
          followerCount: user.FollowerCount,
          isFollowed: user.isFollowed
        }));
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取得美食達人，請稍後再試"
        });
      }
    }
  },
  created() {
    this.fetchUsers();
  }
};
</script>