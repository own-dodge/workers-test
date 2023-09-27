<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {

}
</script>

<style scoped>
.btn {
  padding: 15px;
  background-color: #42b983;
  border: 1px solid #42b983;
  border-radius: 10px;
  color: #fff;
  cursor: pointer;
  transition: ease-in-out .3s;
}

.btn:hover {
  opacity: 0.8;
}
</style>