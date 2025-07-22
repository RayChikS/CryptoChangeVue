<template>
  <div class="container">
    <input
      type="number"
      min="0"
      @input="changeAmount($event.target.value)"
      placeholder="Enter number"
    />
    <button @click="convert()">Convert</button>
    <button @click="favourite()">Add to Favourite</button>
  </div>
</template>

<script>
export default {
  props: {
    changeAmount: {
      type: Function,
      required: true,
    },
    convert: {
      type: Function,
      required: true,
    },
    favourite: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
input {
  width: 500px;
  border-radius: 3px;
  border: none;
  padding: 10px 15px;
  background: #fafafa;
  color: #333;
  outline: none;
  font-size: 1.2em;
}
button {
  margin-top: 20px;
  width: 250px;
  padding: 15px 20px;
  color: #fff;
  text-transform: uppercase;
  background: #1a032d;
  border: 0;
  border-radius: 3px;
  cursor: pointer;
}
button:hover {
  background: #24043e;
}
</style>
