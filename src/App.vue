<template>
  <div>
    <h1>CRYPTO</h1>
    <Input
      :changeAmount="changeAmount"
      :convert="convert"
      :favourite="favourite"
    />
    <p class="error" v-if="error != ''">{{ error }}</p>
    <p class="result" v-if="result != 0">{{ result }}</p>
    <Favourites
      :favs="favs"
      v-if="favs.length > 0"
      :getFromFavs="getFromFavs"
    />
    <div class="selectors">
      <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
      <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
    </div>
  </div>
</template>

<script>
import Input from "./components/Imput.vue";
import Selector from "./components/Selector.vue";
import Favourites from "./components/Favourites.vue";
import CryptoConvert from "crypto-convert";

const convert = new CryptoConvert();

export default {
  components: {
    Input,
    Selector,
    Favourites,
  },
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      favs: [],
    };
  },
  methods: {
    getFromFavs(index) {
      this.cryptoFirst = this.favs[index].from;
      this.cryptoSecond = this.favs[index].to;
    },
    changeAmount(val) {
      this.amount = val;
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val;
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val;
    },
    favourite() {
      if (this.cryptoFirst == "" && this.cryptoSecond == "") {
        this.error = "You need to choose 2 currencyes";
        return;
      } else if (this.cryptoFirst == "" || this.cryptoSecond == "") {
        this.error = "You need to choose 2 currencyes";
        return;
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = "You can't choose same currencyes";
        return;
      } else {
        this.favs.push({
          from: this.cryptoFirst,
          to: this.cryptoSecond,
        });
        this.error = "";
        return;
      }
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
