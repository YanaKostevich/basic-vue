<template>
    <form @submit.prevent>
        <h4>Cтворення поста</h4>
        <my-input
                v-focus
                v-model="post.title"
                @:input="post.title = $event.target.value"
                type="text"
                placeholder="Назва"
        />
        <my-input
                v-model="post.body"
                type="text"
                placeholder="Опис"/>
        <my-button @:click="сreatePost">Створити</my-button>
    </form>
</template>
<script>
import {emit} from "process";

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
