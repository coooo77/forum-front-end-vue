<template>
  <div class="card">
    <div class="card-header">
      <strong>{{Followers.length}}</strong> followers (追隨者)
    </div>
    <div class="card-body">
      <router-link
        v-for="follower in Followers"
        :key="follower.id"
        :to="{name:'user', params:{id:follower.id}}"
      >
        <img :src="follower.image | emptyImage" width="60" height="60" class="avatar" />
      </router-link>
    </div>
  </div>
</template>

<script>
import { emptyImageFilter } from "./../utils/mixins";
export default {
  mixins: [emptyImageFilter],
  props: {
    Followers: {
      type: Array,
      required: true
    }
  }
};
</script>