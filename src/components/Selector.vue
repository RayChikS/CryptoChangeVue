<template>
  <ul>
    <li>Bitcoin</li>
    <li>ETH</li>
    <li>USTD</li>
  </ul>
</template>

<script>
export default {};
</script>

<style scoped>
ul {
  list-style: none;
  width: 200px;
  padding: 0;
  border-radius: 3px;
  border: 3px solid #000;
}
li {
  display: block;
  background: #1a032d;
  color: #fff;
  padding: 20px 0;
}
li:hover,
li:active {
  background: #24043e;
  cursor: pointer;
}
</style>
