<template>
  <div class="app">
    <PostForm @create="сreatePost"/>
    <PostList :posts="posts" />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
export default {
  data() {
    return {
      posts: [
        { id: 1, title: "Vue", body: "Опис поста" },
        { id: 2, title: "Vue 2", body: "Опис поста Vue 2" },
        { id: 3, title: "Vue 3", body: "Опис поста Vue 3" },
      ],
      title: '',
      body:'',
    };
  },
  methods: {
    сreatePost(post) {
      this.posts.push(post);
    },
  },
  components: {
    PostForm,
    PostList,
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  padding: 20px;
}
</style>
