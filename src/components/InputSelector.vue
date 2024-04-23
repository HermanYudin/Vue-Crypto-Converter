<template>
  <div>
    <ul>
      <li
        v-on:click="selectItem('BTC')"
        :class="current == 'BTC' ? 'active' : ''"
      >
        Bitcoin
      </li>
      <li
        v-on:click="selectItem('ETH')"
        :class="current == 'ETH' ? 'active' : ''"
      >
        ETH
      </li>
      <li
        v-on:click="selectItem('USDT')"
        :class="current == 'USDT' ? 'active' : ''"
      >
        USDT
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "InputSelector",
  props: {
    setCrypto: {
      type: Function,
      required: true,
    },
    cryptoNow: {
      type: String,
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
.select-links {
  border-radius: 20px;
  margin-top: 100px;
}

ul {
  list-style: none;
  width: 190px;
  margin-top: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

li {
  display: flex;
  flex-direction: column;
  background-color: white;
  color: deeppink;
  padding: 20px 0;
  transition: all 0.2s ease;
}

li:hover {
  background-color: grey;
  cursor: pointer;
}

.active {
  background-color: grey;
}
</style>
