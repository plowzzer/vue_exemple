<template>
  <div class="repository">
    <Container>
      <header>
        <router-link :to="{ path: `/` }"
          >Voltar para a lista de repositorios</router-link
        >
        <img :src="details.owner.avatar_url" :alt="details.owner.login" />
        <h1>{{ details.name }}</h1>
        <p>{{ details.description }}</p>
      </header>

      <ul class="issueList">
        <li v-for="issue of issues" :key="issue.id">
          <img :src="issue.user.avatar_url" :alt="issue.user.login" />
          <div>
            <strong>
              <a href="issue.html_url">{{ issue.title }}</a>
            </strong>
            <p>{{ issue.user.login }}</p>
          </div>
        </li>
      </ul>
    </Container>
  </div>
</template>

<script>
import Container from '@/components/Container.vue'
import api from '@/services/api.js'

export default {
  components: {
    Container
  },
  data() {
    return {
      repoName: this.$route.params.repo,
      details: {},
      issues: []
    }
  },
  created() {
    this.getRepo()
    this.getIssues()
  },
  methods: {
    async getRepo() {
      const response = await api.get(`/repos/${this.repoName}`)
      this.details = response.data
      // console.log('repository', response)
    },
    async getIssues() {
      const response = await api.get(`/repos/${this.repoName}/issues`)
      this.issues = response.data
      // console.log('issues', response)
    }
  }
}
</script>

<style lang="scss" scoped>
header {
  display: flex;
  flex-direction: column;
  align-items: center;

  a {
    color: #7159c1;
    font-size: 16px;
    text-decoration: none;
  }

  img {
    width: 120px;
    border-radius: 50%;
    margin-top: 20px;
  }

  h1 {
    font-size: 24px;
    margin-top: 10px;
  }

  p {
    margin-top: 5px;
    font-size: 14px;
    color: #666;
    line-height: 1.4;
    text-align: center;
    max-width: 400px;
  }
}
.issueList {
  padding-top: 15px;
  margin-top: 30px;
  border-top: 1px solid #eee;
  list-style: none;

  li {
    display: flex;
    padding: 15px 10px;
    border: 1px solid #eee;
    border-radius: 4px;

    & + li {
      margin-top: 10px;
    }

    img {
      width: 36px;
      height: 36px;
      border-radius: 50%;
      border: 2px solid #eee;
    }

    div {
      flex: 1;
      margin-left: 15px;

      strong {
        font-size: 16px;

        a {
          text-decoration: none;
          color: #333;

          &:hover {
            color: #7159c1;
          }
        }

        span {
          background: #eee;
          color: #333;
          border-radius: 2px;
          font-size: 12px;
          font-weight: 600;
          height: 20px;
          padding: 3px 4px;
          margin-left: 10px;
        }
      }

      p {
        margin-top: 5px;
        font-size: 12px;
        color: #999;
      }
    }
  }
}
</style>
