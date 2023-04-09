<template>
    <div class="app">
        <h1>Сторінка з постами</h1>
        <my-input
                v-model="searchQuery"
                placeholder="Пошук..."
        />
        <div class="app__btns">
            <my-button @click="showDialog">Створити пост</my-button>
            <my-select v-model="selectedSort" :options="sortOptions"/>
        </div>

        <my-dialog v-model:show="dialogVisible">
            <PostForm @create="сreatePost"/>
        </my-dialog>

        <PostList :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostsLoading"/>
        <div v-else>Загрузка...</div>
        <div class="page__wrapper">
            <div
                    v-for="pageNumber in totalPages"
                    :key="pageNumber" class="page"
                    :class="{
                        'current-page': page === pageNumber
                    }"
                    @click="changePage(pageNumber)"
            >
                {{ pageNumber }}
            </div>
        </div>
    </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import axios from "axios";
import MyInput from "@/components/UI/MyInput.vue";

export default {
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostsLoading: false,
            selectedSort: '',
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPages: 0,
            sortOptions: [
                {value: 'title', name: 'По назві'},
                {value: 'body', name: 'По змісту'},
            ],
        };
    },
    methods: {
        сreatePost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter((p) => p.id !== post.id);
        },
        showDialog() {
            this.dialogVisible = true;
        },
        changePage(pageNumber){
            this.page = pageNumber
            this.fetchPosts()
        },
        async fetchPosts() {
            try {
                this.isPostsLoading = true;
                const response = await axios.get(
                    "https://jsonplaceholder.typicode.com/posts", {
                        params: {
                            _page: this.page,
                            _limit: this.limit
                        }
                    }
                );
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                this.posts = response.data;
            } catch (e) {
                alert("Помилка");
            } finally {
                this.isPostsLoading = false;
            }
        },
        // async loadMorePosts() {
        //     try {
        //         this.isPostsLoading = true;
        //         const response = await axios.get(
        //             "https://jsonplaceholder.typicode.com/posts", {
        //                 params: {
        //                     _page: this.page,
        //                     _limit: this.limit
        //                 }
        //             }
        //         );
        //         this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
        //         this.posts = [...this.posts, ...response.data];
        //     } catch (e) {
        //         alert("Помилка");
        //     } finally {
        //         this.isPostsLoading = false;
        //     }
        // },
    },
    mounted() {
        this.fetchPosts();
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    },
    components: {
        MyInput,
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

.app__btns {
    display: flex;
    justify-content: space-between;
    margin: 15px 0;
}

.page__wrapper {
    display: flex;
    margin-top: 15px;
}

.page {
    border: 1px solid #000;
    padding: 10px;
}

.current-page {
    border: 2px solid green;
}
</style>
