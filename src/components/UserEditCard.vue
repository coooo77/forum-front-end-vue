<template>
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
          v-model="userProfile.name"
        />
      </div>

      <div class="form-group">
        <label for="image">Image</label>
        <img
          v-if="userProfile.image"
          :src="userProfile.image"
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

      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    initialUserProfile: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      userProfile: {}
    };
  },
  created() {
    this.fetchUserProfile();
  },
  methods: {
    fetchUserProfile() {
      this.userProfile = this.initialUserProfile;
    },
    handleFileChange(e) {
      const { files } = e.target;

      if (files.length === 0) {
        // 使用者沒有選擇上傳的檔案
        this.userProfile.image = "";
      } else {
        // 否則產生預覽圖
        const imageURL = window.URL.createObjectURL(files[0]);
        this.userProfile.image = imageURL;
      }
    },
    handleSubmit(e) {
      const form = e.target; // <form></form>
      const formData = new FormData(form);
      this.$emit("after-submit", formData);
    }
  }
};
</script>