<template>
  <div class="container py-5">
    <div class="container py-5">
      <form @submit.stop.prevent="handleSubmit">
        <div class="form-group">
          <label for="name">Name</label>
          <input
            id="name"
            type="text"
            name="name"
            class="form-control"
            placeholder="Enter Name"
            required
            v-model="user.name"
          />
        </div>

        <div class="form-group">
          <label for="image">Image</label>
          <img
            v-if="user.image"
            :src="user.image"
            class="d-block img-thumbnail mb-3"
            width="200"
            height="200"
          />
          <input
            id="image"
            type="file"
            name="image"
            accept="image/*"
            class="form-control-file"
            @change="handleFileChange"
          />
        </div>

        <button type="submit" class="btn btn-primary" :disabled="isProcessing">Submit</button>
      </form>
    </div>
    <hr />
  </div>
</template>

<script>
import { mapState } from "vuex";
import usersAPI from "../apis/users";
import { Toast } from "../utils/helpers";

export default {
  computed: {
    ...mapState(["currentUser"])
  },
  data() {
    return {
      user: {
        id: -1,
        name: "",
        image: ""
      },
      isProcessing: false
    };
  },
  methods: {
    async handleSubmit(event) {
      try {
        this.isProcessing = true;

        const form = event.target;
        const formData = new FormData(form);

        if (!formData.get("name")) {
          Toast.fire({
            icon: "warning",
            title: "請填寫使用者名稱"
          });
          return;
        }

        const { data } = await usersAPI.update({
          userId: this.user.id,
          formData
        });

        if (data.status === "error") {
          throw new Error(data.message);
        }

        this.$router.push({ name: "user", params: { id: this.user.id } });
      } catch (error) {
        this.isProcessing = false;
        Toast.fire({
          icon: "error",
          title: "無法更新使用者資料，請稍後再試"
        });
      }
    },
    handleFileChange(e) {
      const { files } = e.target;

      if (files.length === 0) {
        // 使用者沒有選擇上傳的檔案
        this.user.image = "";
      } else {
        // 否則產生預覽圖
        const imageURL = window.URL.createObjectURL(files[0]);
        this.user.image = imageURL;
      }
    },
    setUser(userId) {
      const { id } = this.currentUser;

      // 在 setUser 中判斷該 currentUser 的 id 是否與路由中取得的 userId 相同，如果不是的話，則轉址去 404，否則呼叫 setUser 方法
      if (userId.toString() !== id.toString()) {
        this.$router.push({ name: "not-found" });
        return;
      }
      this.user = {
        ...this.user,
        ...this.currentUser
      };
    }
  },
  created() {
    const { id } = this.$route.params;
    this.setUser(id);
  },
  watch: {
    currentUser(user) {
      // 由於 currentUser 是透過非同步的方式取得，需要透過 watch 屬性來監控當 currentUser 有變更後，需要在呼叫一次 setUser 的方法把資料帶入該 Vue 組件內。
      if (user.id === -1) return;
      const { id } = this.$route.params;
      this.setUser(id);
    }
  }
};
</script>