<template>
    <div v-if="posts.length > 0">
        <h3>Список користувачів</h3>
        <transition-group name="post-list">
            <PostItem :post="post" v-for="post in posts" :key="post.id" @remove="$emit('remove', post)"/>
        </transition-group>
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
<style scoped>
.post-list {
    display: inline-block;
    margin-right: 10px;
}

.post-list-enter-active,
.post-list-leave-active {
    transition: all 0.4s ease;
}

.post-list-enter-from,
.post-list-leave-to {
    opacity: 0;
    transform: translateX(130px);
}

.post-list-move {
    transition: transform 0.4s ease;
}
</style>
