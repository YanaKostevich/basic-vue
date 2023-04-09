<template>
    <div>

        <!--        Приклад роботи store-->
        <!--        <h1>{{ $store.state.isAuth ? "Користувач авторизований" : "Необхідно виконати вхід для користування сервером"}}</h1>-->
        <!--        <h1>{{ $store.getters.doubleLikes }}</h1>-->
        <!--        <div>-->
        <!--            <my-button @click="$store.commit('incrementLikes')">Like</my-button>-->
        <!--            <my-button @click="$store.commit('decrementLikes')">Diselike</my-button>-->
        <!--        </div>-->

        <h1>Сторінка з постами</h1>
        <my-input
                :model-value="searchQuery"
                @update:model-value="setSearchQuery"
                placeholder="Пошук..."
        />
        <div class="app__btns">
            <my-button
                    @click="showDialog"
            >
                Створити пост
            </my-button>
            <my-select
                    :model-value="selectedSort"
                    @update:model-value="setSelectedSort"
                    :options="sortOptions"/>
        </div>

        <my-dialog v-model:show="dialogVisible">
            <PostForm @create="сreatePost"/>
        </my-dialog>

        <PostList :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostsLoading"/>
        <div v-else>Загрузка...</div>
        <div v-intersection="loadMorePosts" class="observer"></div>

    </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import axios from "axios";
import MyInput from "@/components/UI/MyInput.vue";
import MyButton from "@/components/UI/MyButton.vue";
import {mapState, mapActions, mapGetters, mapMutations} from 'vuex'

export default {
    data() {
        return {
            dialogVisible: false,

        };
    },
    methods: {
        ...mapMutations({
            setPage: 'post/setPage',
            setSearchQuery: 'post/setSearchQuery',
            setSelectedSort: 'post/setSelectedSort'
        }),
        ...mapActions({
            loadMorePosts: 'post/loadMorePosts',
            fetchPosts: 'post/fetchPosts'

        }),
        сreatePost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter((p) => p.id !== post.id);
        },
        showDialog() {
            this.dialogVisible = true;
        }
    },
    mounted() {
        this.fetchPosts();
    },
    computed: {
        ...mapState({
            posts: state => state.post.posts,
            isPostsLoading: state => state.post.isPostsLoading,
            selectedSort: state => state.post.selectedSort,
            searchQuery: state => state.post.searchQuery,
            page: state => state.post.page,
            limit: state => state.post.limit,
            totalPages: state => state.post.totalPages,
            sortOptions: state => state.post.sortOptions

        }),
        ...mapGetters({
            sortedPosts: 'post/sortedPosts',
            sortedAndSearchedPosts: 'post/sortedAndSearchedPosts'
        })
    },
    components: {
        MyButton,
        MyInput,
        PostForm,
        PostList,
    },
};
</script>
<style scoped>
.app__btns {
    display: flex;
    justify-content: space-between;
    margin: 15px 0;
}

.observer {

}

/*.page__wrapper {*/
/*    display: flex;*/
/*    margin-top: 15px;*/
/*}*/

/*.page {*/
/*    border: 1px solid #000;*/
/*    padding: 10px;*/
/*}*/

/*.current-page {*/
/*    border: 2px solid green;*/
/*}*/
</style>
