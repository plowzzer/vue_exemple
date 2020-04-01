<template>
  <div class="home">
    <Container>
      <MyInput
        inputName="inputRepository"
        label="Adicione o nome do repositório aqui:"
        v-model="inputValue"
      />
      <MyButton @btnClick="handleSubmit()">Botão</MyButton>
    </Container>
  </div>
</template>

<script>
// @ is an alias to /src
// import api from '@/services/api.js'
import Container from '@/components/Container.vue'
import MyInput from '@/components/MyInput.vue'
import MyButton from '@/components/MyButton.vue'

export default {
  name: 'Home',
  components: {
    Container,
    MyInput,
    MyButton
  },
  data() {
    return {
      inputValue: ''
    }
  },
  methods: {
    handleSubmit() {
      console.log('button hit', this.inputValue)
    }
  }
}
</script>
