<template>
  <h2>Favourites</h2>
  <div v-for="(el, index) in favs" :key="index" @click="getFromFavs(index)">
    <span>{{ el.from }}</span>
    <span>{{ el.to }}</span>
  </div>
</template>

<script>
export default {
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
  color: #fff;
}
div {
  display: flex;
  justify-content: space-between;
  width: 500px;
  margin: 10px auto;
  transition: all 500ms ease;
}
span {
  padding: 10px 15px;
  background: #8c00ff;
  color: #fff;
}
div:hover {
  opacity: 0.7;
  transform: scale(1.1);
  cursor: pointer;
}
</style>
