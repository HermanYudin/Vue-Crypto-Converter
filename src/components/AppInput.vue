<template>
  <div>
    <input
      v-on:input="changeAmount($event.target.value)"
      min="0"
      type="number"
      placeholder="Enter your value"
    />
  </div>
</template>

<script>
export default {
  name: "AppInput",
  props: {
    changeAmount: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
div input {
  min-height: 30px;
  min-width: 300px;
  padding-right: 10px;
  padding-left: 10px;
  outline: none;
  border-radius: 20px;
  border: none;
  color: deeppink;
}
</style>
