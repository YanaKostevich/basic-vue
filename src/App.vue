<template>
  <div class="app">
    <h1>Сторінка з постами</h1>
    <!-- <MyButton @click="fetchPosts" style="margin: 15px 0;">Переглянути пости</MyButton> -->
    <MyButton @click="showDialog" style="margin: 15px 0;">Створити пост</MyButton>
    <my-dialog v-model:show="dialogVisible">
      <PostForm @create="сreatePost"/>
    </my-dialog>
    
    <PostList :posts="posts" @remove="removePost" v-if="!isPostsLoading"/>
    <div v-else>Загрузка...</div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import axios from 'axios';
export default {
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
    };
  },
  methods: {
    сreatePost(post) {
      this.posts.push(post);
      this.dialogVisible = false
    },
    removePost(post){
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts(){
      try{
        this.isPostsLoading = true;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
        this.posts = response.data;
        
      }catch (e){
        alert('Помилка')
      } finally{
        this.isPostsLoading = false;
      }
    }
  },
  mounted(){
    this.fetchPosts()
  },
  components: {
    PostForm,
    PostList
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
