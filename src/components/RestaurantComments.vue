<template>
  <div>
    <h2 class="my-4">所有評論：</h2>

    <div v-for="comment in restaurantComments" :key="comment.id">
      <blockquote class="blockquote mb-0">
        <button
          v-if="currentUser.isAdmin"
          type="button"
          class="btn btn-danger float-right"
          @click.stop.prevent="handleDeleteButtonClick(comment.id)"
        >Delete</button>
        <h3>
          <router-link :to="{name:'user', params:{id:comment.User.id}}">{{comment.User.name}}</router-link>
        </h3>
        <p>{{comment.text}}</p>
        <footer class="blockquote-footer">{{ comment.createdAt | fromNow }}</footer>
      </blockquote>
      <hr />
    </div>
  </div>
</template>

<script>
import { fromNowFilter } from "./../utils/mixins";
import { mapState } from "vuex";
import AdminAPI from "../apis/admin";
import { Toast } from "../utils/helpers";

export default {
  name: "RestaurantComments",
  props: {
    restaurantComments: {
      type: Array,
      required: true
    }
  },
  computed: {
    ...mapState(["currentUser"])
  },
  mixins: [fromNowFilter],
  methods: {
    async handleDeleteButtonClick(commentId) {
      try {
        if (!this.currentUser.isAdmin) {
          Toast.fire({
            icon: "error",
            title: "需要管理員身分才能刪除留言"
          });
          return;
        }
        // TODO: 請求 API 伺服器刪除 id 為 commentId 的評論
        const { data } = await AdminAPI.comments.delete(commentId);

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        // 觸發父層事件 - $emit( '事件名稱' , 傳遞的資料 )
        // U112 在父元件Restaurant.vue請求伺服器刪除資料 或 在子元件 RestaurantComments.vue請求伺服器刪除資料 兩者有差別嗎?
        this.$emit("after-delete-comment", commentId);
      } catch (error) {
        console.error(error);
        Toast.fire({
          icon: "warning",
          title: "無法刪除留言，請稍後嘗試"
        });
      }
    }
  }
};
</script>