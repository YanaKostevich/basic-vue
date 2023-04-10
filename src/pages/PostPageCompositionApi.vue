<template>
    <div>

        <h1>Сторінка з постами</h1>
        <my-input
                v-model="searchQuery"
                placeholder="Пошук..."
        />
        <div class="app__btns">
            <my-select v-model="selectedSort" :options="sortOptions"/>
        </div>

        <my-dialog v-model:show="dialogVisible">
        </my-dialog>

        <PostList :posts="sortedAndSearchedPosts" v-if="!isPostsLoading"/>
        <div v-else>Загрузка...</div>

    </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import axios from "axios";
import MyInput from "@/components/UI/MyInput.vue";
import {ref} from "vue";
import {usePosts} from "@/hooks/usePosts";
import useSortedPosts from "@/hooks/useSortedPosts";
import useSortedAndSearchedPosts from "@/hooks/useSortedAndSearchedPosts";

export default {
    data() {
        return {
            dialogVisible: false,
            sortOptions: [
                {value: 'title', name: 'По назві'},
                {value: 'body', name: 'По змісту'},
            ],
        };
    },
    setup(props){
        const {posts, totalPages, isPostsLoading} = usePosts(10);
        const {selectedSort, sortedPosts} = useSortedPosts(posts);
        const {searchQuery, sortedAndSearchedPosts} = useSortedAndSearchedPosts(sortedPosts);

        return {
            posts,
            totalPages,
            isPostsLoading,
            selectedSort,
            sortedPosts,
            searchQuery,
            sortedAndSearchedPosts

        }
    },

    components: {
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
