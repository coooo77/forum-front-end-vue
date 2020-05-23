<template>
  <div class="col-3">
    <a href="#">
      <img :src="topUser.image | emptyImage" width="180px" height="180px" />
    </a>
    <h2>{{user.name}}</h2>
    <span class="badge badge-secondary">追蹤人數：{{topUser.followerCount}}</span>
    <p class="mt-3">
      <button
        v-if="topUser.isFollowed"
        type="button"
        class="btn btn-danger"
        @click.stop.prevent="unFollow(user.id)"
      >取消追蹤</button>
      <button v-else type="button" class="btn btn-primary" @click.stop.prevent="follow(user.id)">追蹤</button>
    </p>
  </div>
</template>

<script>
import { emptyImageFilter } from "./../utils/mixins";
import usersAPI from "../apis/users";
import { Toast } from "../utils/helpers";

export default {
  mixins: [emptyImageFilter],
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      topUser: this.user
    };
  },
  methods: {
    async follow(userId) {
      try {
        const { data } = await usersAPI.addFollowing({ userId });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.topUser = {
          ...this.topUser,
          followerCount: ++this.topUser.followerCount,
          isFollowed: true
        };
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法加入追蹤，請稍後再試"
        });
      }
    },
    async unFollow(userId) {
      try {
        const { data } = await usersAPI.deleteFollowing({ userId });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.topUser = {
          ...this.topUser,
          followerCount: --this.topUser.followerCount,
          isFollowed: false
        };
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法取消追蹤，請稍後再試"
        });
      }
    }
  }
};
</script>