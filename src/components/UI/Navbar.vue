<template>
    <div class="navbar">
        <div @click="$router.push('/')">Vue 3</div>
        <div class="navbar__btns">
            <my-button @click="$router.push('/about')">Про сайт</my-button>
            <my-button @click="$router.push('/posts')" style="margin-left: 15px">Пости</my-button>
            <my-button @click="$router.push('/store')" style="margin-left: 15px">Store</my-button>
        </div>
    </div>
</template>

<script>

export default {}
</script>

<style scoped>
.navbar {
    padding: 50px 50px;
    height: 50px;
    background-color: aliceblue;
    box-shadow: 2px 2px 4px darkgrey;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>