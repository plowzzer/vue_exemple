<template>
  <div class="home">
    <Container>
      <div class="form">
        <div class="inputRepository">
          <MyInput
            inputName="inputRepository"
            label="Adicione o nome do repositório aqui:"
            ref="repoInput"
            v-model="inputValue"
            @keyup.enter.native="handleSubmit"
          />
          <p v-if="errorMessage">{{ errorMessage }}</p>
        </div>
        <MyButton @btnClick="handleSubmit()" type="btn-success">
          +
        </MyButton>
      </div>

      <hr />

      <ul class="repository-list">
        <li v-for="repository of repositories" :key="repository">
          <router-link
            :to="{ path: `/repository/${encodeURIComponent(repository)}` }"
            >{{ repository }}</router-link
          >
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
    // Handle focus on input after this component is mounted
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
          this.handleClean()
          this.inputValue = ''
          this.errorMessage = ''
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

<style lang="scss">
.form {
  display: flex;
  align-items: center;
  .inputRepository {
    flex: 1;
    margin-right: 15px;
  }
  button {
    height: 44px;
  }
}
ul.repository-list {
  li {
    padding: 20px 5px;
    border-bottom: 1px solid #eee;
    &:last-child {
      border-bottom: none;
    }
    a {
      color: #42b983;
      font-size: 16px;
      padding: 5px;
    }
  }
}
</style>
