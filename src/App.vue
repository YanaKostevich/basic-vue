<template>
  <div>
    <div>
      <button @:click="likes += 1">Likes</button>
      <button @:click="dislikes += 1">DisLikes</button>
    </div>

    <div>
      Likes <strong> {{ likes }}</strong>
    </div>
    <div>
      DisLikes <strong> {{ dislikes }}</strong>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      likes: 0,
      dislikes: 0,
    };
  },
};
</script>
<style></style>
