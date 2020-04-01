<template>
  <button class="button" :class="type" @click="handleClick()">
    <slot />
  </button>
</template>

<script>
export default {
  props: {
    type: String
  },
  methods: {
    handleClick() {
      this.$emit('btnClick')
    }
  }
}
</script>

<style lang="scss">
.button {
  background: #2c3e50;
  border: 0;
  padding: 6px 12px;
  margin: 5px 0;
  font-size: 14px;
  font-weight: bold;
  border-radius: 4px;
  text-transform: uppercase;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
