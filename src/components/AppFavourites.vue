<template>
  <div>
    <h2>Your favourites :</h2>
    <div @click="getFromFavs(index)" v-for="(fav, index) in favs" :key="index">
      <div class="your-favs-list">
        <span class="favs-item">{{ fav.from }}</span>
        <span>&nbsp;&nbsp;to&nbsp;&nbsp;</span>
        <span class="favs-item">{{ fav.to }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppFavourites",
  props: {
    favs: {
      type: Array,
      required: true,
    },
    getFromFavs: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
h2 {
  border-bottom: 2px solid deeppink;
  max-width: 190px;
  margin: 0 auto;
  margin-top: 20px;
}

.your-favs-list {
  margin-top: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.favs-item {
  margin-top: 10px;
  font-size: 22px;
  color: white;
  background-color: deeppink;
  border: 2px solid white;
  padding: 4px 8px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.favs-item:hover {
  background-color: grey;
}
</style>
