<template>
  <div id="app">
    <h1 class="main-title">CRYPTO</h1>
    <AppInput
      v-bind:changeAmount="changeAmount"
      v-bind:covert="convert"
      v-bind:favourites="favourites"
    />
    <p class="result" v-if="result != 0">Your result: {{ result }}</p>
    <p class="errorMessage" v-if="error != ''">{{ error }}</p>
    <AppButton v-bind:convert="convert" />
    <AppFavourites :favs="favs" getFromFavs="getFromFavs" />
    <div class="selectors">
      <div>
        <h2 class="convert-header">First convert value</h2>
        <InputSelector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
      </div>
      <p class="convert-to">TO</p>
      <div>
        <h2 class="convert-header">Second convert value</h2>
        <InputSelector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
      </div>
    </div>
  </div>
</template>

<script>
import AppInput from "../components/AppInput.vue";
import InputSelector from "../components/InputSelector.vue";
import AppButton from "../components/AppButton.vue";
import AppFavourites from "../components/AppFavourites.vue";
import CryptoConvert from "crypto-convert";

const convert = new CryptoConvert();

export default {
  components: {
    AppInput,
    InputSelector,
    AppButton,
    AppFavourites,
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
    favorites() {
      if (
        this.cryptoFirst !== "" &&
        this.cryptoSecond !== "" &&
        this.cryptoFirst !== this.cryptoSecond
      ) {
        this.favs.push({
          from: this.cryptoFirst,
          to: this.cryptoSecond,
        });
      }
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
    async convert() {
      if (this.amount <= 0) {
        this.error = "Please enter correct value";
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = "Please choose another second or first convert value";
      } else if (this.cryptoFirst == "" || this.cryptoSecond == "") {
        this.error = "Please choose convert values";
      } else {
        this.error = "";
      }

      await convert.ready();

      if (this.cryptoFirst == "BTC" && this.cryptoSecond == "ETH") {
        this.result = convert.BTC.ETH(this.amount);
      } else if (this.cryptoFirst == "BTC" && this.cryptoSecond == "USDT") {
        this.result = convert.BTC.USDT(this.amount);
      } else if (this.cryptoFirst == "ETH" && this.cryptoSecond == "BTC") {
        this.result = convert.ETH.BTC(this.amount);
      } else if (this.cryptoFirst == "ETH" && this.cryptoSecond == "USDT") {
        this.result = convert.ETH.USDT(this.amount);
      } else if (this.cryptoFirst == "USDT" && this.cryptoSecond == "BTC") {
        this.result = convert.USDT.BTC(this.amount);
      } else if (this.cryptoFirst == "USDT" && this.cryptoSecond == "ETH") {
        this.result = convert.USDT.ETH(this.amount);
      }
    },
  },
};
</script>

<style scoped>
#app {
  min-width: 800px;
  min-height: 500px;
  background: rgb(174, 238, 199);
  background: linear-gradient(
    90deg,
    rgba(174, 238, 199, 1) 11%,
    rgba(148, 187, 233, 1) 99%
  );
  border-radius: 50px;
  align-items: center;
  text-align: center;
  padding-bottom: 35px;
}

.main-title {
  font-size: 40px;
  margin-top: 20px;
  margin-bottom: 20px;
}

.selectors {
  display: flex;
  justify-content: space-around;
  width: 400px;
  margin: 0 auto;
  margin-top: 20px;
}

.errorMessage {
  margin-top: 20px;
}

.convert-header {
  font-size: 15px;
  border-bottom: 2px solid deeppink;
  padding-bottom: 5px;
}

.convert-to {
  margin-top: 121px;
  margin-right: 20px;
  margin-left: 20px;
  min-width: 60px;
  max-height: 50px;
  border: 2px solid white;
  padding: 10px;
  color: white;
  background: deeppink;
}

.result {
  margin-top: 20px;
}

.favorites-button {
  min-width: 100px;
  min-height: 30px;
  margin-top: 20px;
  color: deeppink;
  border: none;
  font-weight: bold;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.favorites-button:hover {
  background-color: grey;
}
</style>
../components/AppInput.vue../components/AppFavourites.vue
