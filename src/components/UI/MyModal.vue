<template>
  <div class="modal" v-if="show" @click="hideModal">
    <div @click.stop class="modal__content">
      <slot></slot>
    </div>
  </div>

</template>

<script>
export default {
  name: "MyModal",
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hideModal() {
      this.$emit('update:show', false)
    }
  }
}
</script>

<style scoped>
.modal {
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background: rgba(0,0,0, 0.6);
  position: fixed;
  display: flex;
}

.modal__content {
  margin: auto;
  background-color: #ffffff;
  border-radius: 10px;
  min-height: 60px;
  min-width: 350px;
  padding: 15px 20px;
}

</style>