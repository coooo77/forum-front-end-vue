<template>
  <div>
    <div class="album py-5 bg-light">
      <div class="container">
        <!-- UserProfileCard -->
        <UserProfileCard
          :initialProfile="profile"
          :initialIsFollowed="isFollowed"
          @after-follow="afterFollow"
          @after-unfollow="afterUnfollow"
        />
        <div class="row">
          <div class="col-md-4">
            <!-- UserFollowingsCard -->
            <UserFollowingsCard :Followings="profile.Followings" />
            <br />
            <!-- UserFollwersCard -->
            <UserFollowersCard :Followers="profile.Followers" />
          </div>
          <div class="col-md-8">
            <!-- UserCommentsCard -->
            <UserCommentsCard :Comments="profile.Comments" />
            <br />
            <!-- UserFavoritedRestaurantsCard -->
            <UserFavoritedRestaurantsCard :FavoritedRestaurants="profile.FavoritedRestaurants" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UserProfileCard from "./../components/UserProfileCard";
import UserFollowingsCard from "./../components/UserFollowingsCard";
import UserFollowersCard from "./../components/UserFollowersCard";
import UserCommentsCard from "./../components/UserCommentsCard";
import UserFavoritedRestaurantsCard from "./../components/UserFavoritedRestaurantsCard";
import usersAPI from "../apis/users";
import { Toast } from "../utils/helpers";
import { mapState } from "vuex";

export default {
  name: "userProfile",
  components: {
    UserProfileCard,
    UserFollowingsCard,
    UserFollowersCard,
    UserCommentsCard,
    UserFavoritedRestaurantsCard
  },
  computed: {
    ...mapState(["currentUser"])
  },
  data() {
    return {
      profile: {},
      isFollowed: false
    };
  },
  methods: {
    async fetchUser(userId) {
      try {
        const { data } = await usersAPI.get({ userId });

        if (data.status === "error") {
          throw new Error(data.message);
        }

        const { profile, isFollowed } = data;

        profile.Comments = profile.Comments.filter(
          Comment => Comment.Restaurant
        );

        this.profile = profile;
        this.isFollowed = isFollowed;
      } catch (error) {
        console.error(error);
        Toast.fire({
          icon: "error",
          title: "找不到使用者資料，請稍後嘗試"
        });
      }
    },
    afterFollow(playload) {
      this.isFollowed = playload.isFollowed;
    },
    afterUnfollow(playload) {
      this.isFollowed = playload.isFollowed;
    }
  },
  created() {
    const { id } = this.$route.params;
    this.fetchUser(id);
  },
  beforeRouteUpdate(to, from, next) {
    const { id } = to.params;
    this.fetchUser(id);
    next();
  }
};
</script>