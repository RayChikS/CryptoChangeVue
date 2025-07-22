<template>
  <div>
    <h1>CRYPTO</h1>
    <Input :changeAmount="changeAmount" :convert="convert" />
    <p class="error" v-if="error != ''">{{ error }}</p>
    <p class="result" v-if="result != 0">{{ result }}</p>
    <div class="selectors">
      <Selector :setCrypto="setCryptoFirst" />
      <Selector :setCrypto="setCryptoSecond" />
    </div>
  </div>
</template>

<script>
import Input from "./components/Imput.vue";
import Selector from "./components/Selector.vue";
import CryptoConvert from "crypto-convert";

const convert = new CryptoConvert();

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
      result: 0,
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
    async convert() {
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

      await convert.ready();

      if (
        this.cryptoFirst &&
        this.cryptoSecond &&
        convert[this.cryptoFirst] &&
        convert[this.cryptoFirst][this.cryptoSecond]
      ) {
        this.result = convert[this.cryptoFirst][this.cryptoSecond](this.amount);
      } else {
        this.result = 0;
      }
    },
  },
};
</script>

<style scoped>
.result {
  font-family: "Nabla", system-ui;
  font-size: 2em;
}
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
