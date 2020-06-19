<template>
  <div class="card">
    <div class="card-header">
      <strong>{{Comments.length}}</strong> 已評論餐廳
    </div>
    <div class="card-body">
      <router-link
        v-for="comment in Comments"
        :key="comment.id"
        :to="{name:'restaurant', params:{id:comment.Restaurant.id}}"
      >
        <img :src="comment.Restaurant.image | emptyImage" width="60" height="60" class="avatar" />
      </router-link>
    </div>
  </div>
</template>

<script>
import { emptyImageFilter } from "./../utils/mixins";
export default {
  mixins: [emptyImageFilter],
  props: {
    Comments: {
      type: Array,
      required: true
    }
  }
};
</script>