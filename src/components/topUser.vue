<template>
  <div class="col-3">
    <a href="#">
      <img :src="topUser.image | emptyImage" width="180px" height="180px" />
    </a>
    <h2>{{user.name}}</h2>
    <span class="badge badge-secondary">追蹤人數：{{topUser.FollowerCount}}</span>
    <p class="mt-3">
      <button
        v-if="topUser.isFollowed"
        type="button"
        class="btn btn-danger"
        @click.stop.prevent="unFollow"
      >取消追蹤</button>
      <button v-else type="button" class="btn btn-primary" @click.stop.prevent="follow">追蹤</button>
    </p>
  </div>
</template>

<script>
import { emptyImageFilter } from "./../utils/mixins";
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
    follow() {
      // 如果我不直接用template，可以直接再UsersTop.vue做出topUsers嗎?
      this.topUser = {
        ...this.topUser,
        FollowerCount: ++this.topUser.FollowerCount,
        isFollowed: true
      };
    },
    unFollow() {
      this.topUser = {
        ...this.topUser,
        FollowerCount: --this.topUser.FollowerCount,
        isFollowed: false
      };
    }
  }
};
</script>