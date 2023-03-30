<template>
  <div>
    <h3>Список користувачів</h3>
    <PostItem :post="post" v-for="post in posts" />
  </div>
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
