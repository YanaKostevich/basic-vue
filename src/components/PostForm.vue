<template>
  <form @submit.prevent>
    <h4>створення поста</h4>
    <input
      v-model="post.title"
      @:input="post.title = $event.target.value"
      class="input"
      type="text"
      placeholder="Назва"
    />
    <input v-model="post.body" class="input" type="text" placeholder="Опис" />
    <MyButton class="btn" @:click="сreatePost">Створити</MyButton>
  </form>
</template>
<script>
import { emit } from 'process';
import MyButton from "@/components/UI/MyButton.vue";
export default {
  components:{
    MyButton
  },
  data() {
    return {
      post: {
        title: '',
        body: '',
      },
    };
  },
  methods:{
    сreatePost(){
      this.post.id = Date.now();
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: '',
      }
    }
  }

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
.input {
  width: 100%;
  border: 1px solid green;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>
