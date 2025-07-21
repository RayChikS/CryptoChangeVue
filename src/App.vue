<template>
  <div>
    <h1>CRYPTO</h1>
    <Input />
    <div class="selectors">
      <Selector />
      <Selector />
    </div>
  </div>
</template>

<script>
import Input from "./components/Imput.vue";
import Selector from "./components/Selector.vue";

export default {
  components: {
    Input,
    Selector,
  },
};
</script>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-between;
  max-width: 500px;
  margin: 0 auto;
}
</style>
