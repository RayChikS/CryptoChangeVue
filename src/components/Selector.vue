<template>
  <ul>
    <li @click="selectItem('BTC')" :class="current == 'BTC' ? 'active' : ''">
      Bitcoin
    </li>
    <li @click="selectItem('ETH')" :class="current == 'ETH' ? 'active' : ''">
      ETH
    </li>
    <li @click="selectItem('USDT')" :class="current == 'USDT' ? 'active' : ''">
      USDT
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    setCrypto: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      current: "",
    };
  },
  methods: {
    selectItem(val) {
      this.setCrypto(val);
      this.current = val;
    },
  },
};
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
li.active {
  background: #24043e;
  cursor: pointer;
}
</style>
