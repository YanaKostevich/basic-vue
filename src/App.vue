<template>
  <div class="app">
    <form @submit.prevent>
      <h4>створення поста</h4>
      <input
        v-bind:value="title"
        @:input="title = $event.target.value"
        class="input"
        type="text"
        placeholder="Назва"
      />
      <input
        v-bind:value="body"
        @:input="body = $event.target.value"
        class="input"
        type="text"
        placeholder="Опис"
      />
      <button class="btn" @:click="сreatePost">Створити</button>
    </form>

    <div class="post" v-for="post in posts">
      <div><strong>Назва: </strong>{{ post.title }}</div>
      <div><strong>Опис: </strong>{{ post.body }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [
        { id: 1, title: "Vue", body: "Опис поста" },
        { id: 2, title: "Vue 2", body: "Опис поста Vue 2" },
        { id: 3, title: "Vue 3", body: "Опис поста Vue 3" },
      ],
      title: '',
      body: '',
    }
  },
  methods: {
    сreatePost() {
      const newPost = {
        id: Date.now(),
        title: this.title,
        body: this.body,
      }
      this.posts.push(newPost);
      this.title = '';
      this.body = '';
    },
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.post {
  padding: 15px;
  border: 2px solid green;
  margin-top: 15px;
}
.app {
  padding: 20px;
}
form {
  display: flex;
  flex-direction: column;
}
.btn {
  margin-top: 15px;
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  color: green;
  border: 1px solid green;
}
.input {
  width: 100%;
  border: 1px solid green;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>
