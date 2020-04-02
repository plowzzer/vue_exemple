<template>
  <div class="home">
    <Container>
      <MyInput
        inputName="inputRepository"
        label="Adicione o nome do repositório aqui:"
        ref="repoInput"
        v-model="inputValue"
      />
      <p v-if="errorMessage">{{ errorMessage }}</p>
      <MyButton @btnClick="handleSubmit()" type="btn-success">Botão</MyButton>
      <MyButton @btnClick="handleFocus()">Focus</MyButton>

      <hr />

      <ul>
        <li v-for="repository of repositories" :key="repository">
          {{ repository }}
        </li>
      </ul>
    </Container>
  </div>
</template>

<script>
// @ is an alias to /src
import api from '@/services/api.js'
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
      inputValue: '',
      repositories: [],
      errorMessage: ''
    }
  },
  created() {
    // Get repositories from my localstorage
    const repositoriesJson = localStorage.getItem('repositories')
    if (repositoriesJson) {
      this.repositories = JSON.parse(repositoriesJson)
    }
  },
  mounted() {
    this.handleFocus()
  },
  methods: {
    // Adding a repository
    async handleSubmit() {
      try {
        if (this.inputValue === '') {
          this.errorMessage = 'Você precisa preencher o nome de um repositorio'
          return
        }
        const response = await api.get(`/repos/${this.inputValue}`)
        if (response.status === 200) {
          this.repositories = [...this.repositories, response.data.full_name]
          localStorage.setItem(
            'repositories',
            JSON.stringify(this.repositories)
          )
          this.inputValue = ''
        }
      } catch (error) {
        console.error(error)
        this.errorMessage = 'Você precisa preencher o nome de um repositorio'
      }
    },
    handleFocus() {
      this.$refs.repoInput.handleFocus()
    }
  }
}
</script>
