<template>
  <div class="input-field">
    <label :for="inputName">{{ label }}</label>
    <input
      :id="inputName"
      :value="inputValue"
      @input="handleInput($event.target.value)"
      @focus="handleFocus($event)"
    />
  </div>
</template>

<script>
export default {
  props: {
    inputName: String,
    inputValue: String,
    label: String
  },
  methods: {
    handleInput(value) {
      this.$emit('input', value)
    },
    handleFocus() {
      console.log('handlefocus', this.$el.children[1].focus())
    }
  },
  created() {
    console.log('created', this.inputRef)
  }
}
</script>

<style lang="scss">
.input-field {
  label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px;
    text-align: left;
    color: #444;
  }

  input {
    width: 100%;
    margin-bottom: 15px;
    border-radius: 4px;
    border: 1px solid #ddd;
    font-size: 15px;
    color: #444;
    transition: border-color 0.3s;
    padding: 12px 16px;
    &:focus {
      border-radius: #2c3e50;
    }
  }
}
</style>
