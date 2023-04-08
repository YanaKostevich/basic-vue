<template>
  <div v-if="posts.length > 0">
    <h3>Список користувачів</h3>
    <PostItem :post="post" v-for="post in posts" :key="post.id" @remove="$emit('remove', post)" />
  </div>
  <h2 v-else style="color: red">
    Список постів пустий
  </h2>
</template>

<script>
import PostItem from "@/components/PostItem.vue";
export default {
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
  components: {
    PostItem,
  },
};
</script>
<style scoped></style>
