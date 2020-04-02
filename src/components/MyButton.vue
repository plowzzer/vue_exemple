<template>
  <button class="btn" :class="type" @click="handleClick()">
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
.btn {
  background: #2c3e50;
  border: none;
  padding: 6px 12px;
  margin: 5px 0;
  font-size: 14px;
  font-weight: bold;
  border-radius: 4px;
  text-transform: uppercase;
  color: white;
  transition: 0.4s all;
  &:hover {
    background: #1b2d3f;
  }
  &.btn-success {
    background: #42b983;
    &:hover {
      background: #31a872;
    }
  }
}
</style>
