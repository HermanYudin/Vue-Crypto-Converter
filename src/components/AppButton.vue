<template>
  <div>
    <button @click="convert()">CONVERT</button>
  </div>
</template>

<script>
export default {
  name: "AppButton",
  props: {
    convert: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
button {
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

button:hover {
  background-color: grey;
}
</style>
