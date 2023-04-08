<template>
  <form @submit.prevent>
    <h4>Cтворення поста</h4>
    <MyInput
      v-model="post.title"
      @:input="post.title = $event.target.value"
      type="text"
      placeholder="Назва"
    />
    <MyInput 
      v-model="post.body"
      type="text"
      placeholder="Опис" />
    <MyButton @:click="сreatePost">Створити</MyButton>
  </form>
</template>
<script>
import { emit } from "process";

export default {
  data() {
    return {
      post: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    сreatePost() {
      this.post.id = Date.now();
      this.$emit("create", this.post);
      this.post = {
        title: "",
        body: "",
      };
    },
  },
};
</script>
<style scoped>
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

</style>
