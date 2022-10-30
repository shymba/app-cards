<template>
  <button class="btn">
    <slot></slot>
  </button>

</template>

<script>
export default {
  name: "MyBtn"
}
</script>

<style scoped>
.btn {
  align-self: flex-end;
  margin: 10px;
  padding: 10px;
  background: none;
  color: olive;
  border: 1px solid olive;
  border-radius: 4px;
  cursor: pointer;
}
.btn:hover,
.btn:focus {
  color: #ffffff;
  background-color: olive;
}

</style>