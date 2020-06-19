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
            <button
              type="submit"
              class="btn btn-danger"
              @click.stop.prevent="deleteFollowing(profile.id)"
            >取消追蹤</button>
          </form>
          <form v-else action="/following/3" method="POST" style="display: contents;">
            <button
              type="submit"
              class="btn btn-primary"
              @click.stop.prevent="addFollowing(profile.id)"
            >追蹤</button>
          </form>
          <p></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { emptyImageFilter } from "./../utils/mixins";
import usersAPI from "../apis/users";
import { Toast } from "../utils/helpers";
import { mapState } from "vuex";

export default {
  mixins: [emptyImageFilter],
  props: {
    initialProfile: {
      type: Object,
      required: true,
      default: () => ({
        id: -1,
        name: "",
        email: "",
        Comments: [],
        FavoritedRestaurants: [],
        Followings: [],
        Followers: []
      })
    },
    initialIsFollowed: {
      type: Boolean,
      required: false
    }
  },
  computed: {
    ...mapState(["currentUser"])
  },
  created() {
    Object.assign(this.profile, this.initialProfile);
    this.isFollowed = this.initialIsFollowed;
  },
  data() {
    return {
      profile: {
        id: -1,
        name: "",
        email: "",
        Comments: [],
        FavoritedRestaurants: [],
        Followings: [],
        Followers: []
      },
      isFollowed: false
    };
  },
  methods: {
    async addFollowing(id) {
      try {
        const { data } = await usersAPI.addFollowing({ userId: id });

        if (data.status !== "success") {
          throw new Error(data.statusText);
        }

        this.$emit("after-follow", {
          isFollowed: true
        });
      } catch (error) {
        console.error(error);
        Toast.fire({
          icon: "error",
          title: "無法追蹤，請稍後再試"
        });
      }
    },
    async deleteFollowing(id) {
      try {
        const { data } = await usersAPI.deleteFollowing({ userId: id });

        if (data.status !== "success") {
          throw new Error(data.statusText);
        }

        this.$emit("after-unfollow", {
          isFollowed: false
        });
      } catch (error) {
        console.error(error);
        Toast.fire({
          icon: "error",
          title: "無法取消追蹤，請稍後再試"
        });
      }
    }
  },
  watch: {
    initialProfile(newValue, oldValue) {
      console.log("profile newValue", newValue, "oldValue", oldValue);

      this.profile = newValue;
    },
    initialIsFollowed(newValue, oldValue) {
      console.log("isFollowed newValue", newValue, "oldValue", oldValue);

      this.isFollowed = newValue;
    }
  }
};
</script>