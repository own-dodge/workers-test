<template>
  <div class="modal" v-if="show" @click="closeModal">
    <div @click.stop class="modal-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalComponent',
  props: {
    show: {
      type: Boolean,
      default: false,
    }
  },
  methods: {
    closeModal() {
      this.$emit('update:show', false)
    }
  }
}
</script>

<style scoped>
.modal {
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.6);
  position: fixed;
  display: flex;
}

.modal-content {
  margin: auto;
  padding: 30px;
  width: 500px;
  background-color: white;
  border-radius: 10px;
}
</style>