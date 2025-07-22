<template>
  <div>
    <h1>CRYPTO</h1>
    <Input :changeAmount="changeAmount" :convert="convert" />
    <p class="error" v-if="error != ''">{{ error }}</p>
    <div class="selectors">
      <Selector :setCrypto="setCryptoFirst" />
      <Selector :setCrypto="setCryptoSecond" />
    </div>
  </div>
</template>

<script>
import Input from "./components/Imput.vue";
import Selector from "./components/Selector.vue";
import CryptoConvert from 'crypto-convert';

export default {
  components: {
    Input,
    Selector,
  },
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
    };
  },
  methods: {
    changeAmount(val) {
      this.amount = val;
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val;
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val;
    },
    convert() {
      if (this.amount <= 0) {
        this.error = "Enter number more than 0";
        return;
      } else if (this.cryptoFirst == "" && this.cryptoSecond == "") {
        this.error = "Choose currency";
        return;
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = "Can't convert same currency";
        return;
      } else if (this.cryptoFirst == "" || this.cryptoSecond == "") {
        this.error = "Choose second currency";
        return;
      }
      this.error = "";
    },
  },
};
</script>

<style scoped>
.error {
  font-size: 20px;
  font-weight: 600;
  color: #e20a0a;
}
.selectors {
  display: flex;
  justify-content: space-between;
  max-width: 500px;
  margin: 0 auto;
}
</style>
