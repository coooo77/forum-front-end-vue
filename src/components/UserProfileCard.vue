<template>
  <div class="card mb-3">
    <div class="row no-gutters">
      <div class="col-md-4">
        <img :src="profile.image | emptyImage" width="300px" height="300px" />
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{profile.name}}</h5>
          <p class="card-text">{{profile.email}}</p>
          <ul class="list-unstyled list-inline">
            <li>
              <strong>{{profile.Comments.length}}</strong> 已評論餐廳
            </li>
            <li>
              <strong>{{profile.FavoritedRestaurants.length}}</strong> 收藏的餐廳
            </li>
            <li>
              <strong>{{profile.Followings.length}}</strong>
              followings (追蹤者)
            </li>
            <li>
              <strong>{{profile.Followers.length}}</strong>
              followers (追隨者)
            </li>
          </ul>
          <p></p>
          <router-link
            v-if="currentUser.id === profile.id"
            class="btn btn-primary btn-border mr-2"
            :to="{ name: 'user-edit', params: { id: currentUser.id }} "
          >Edit</router-link>
          <form
            v-else-if="isFollowed"
            action="/following/3"
            method="POST"
            style="display: contents;"
          >
            <button type="submit" class="btn btn-danger" @click.stop.prevent="deleteFollowing">取消追蹤</button>
          </form>
          <form v-else action="/following/3" method="POST" style="display: contents;">
            <button type="submit" class="btn btn-primary" @click.stop.prevent="addFollowing">追蹤</button>
          </form>
          <p></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { emptyImageFilter } from "./../utils/mixins";
const dummyUser = {
  currentUser: {
    id: 1,
    name: "管理者",
    email: "root@example.com",
    image: "https://i.pravatar.cc/300",
    isAdmin: true
  },
  isAuthenticated: true
};

export default {
  mixins: [emptyImageFilter],
  props: {
    profile: {
      type: Object,
      required: true
    },
    isFollowed: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      currentUser: {}
    };
  },
  methods: {
    fetchUser() {
      this.currentUser = dummyUser.currentUser;
    },
    addFollowing() {
      this.$emit("after-follow", {
        isFollowed: true
      });
    },
    deleteFollowing() {
      this.$emit("after-unfollow", {
        isFollowed: false
      });
    }
  },
  created() {
    this.fetchUser();
  }
};
</script>