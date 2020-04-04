<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Main</router-link> |
      <router-link to="/repository">Repository</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  outline: 0;
  box-sizing: border-box;
}
*:focus {
  outline: 0;
}

html,
body,
#root {
  height: 100%;
}

body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body,
input,
button {
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
  font-size: 14px;
}

a {
  text-decoration: none;
}

ul {
  list-style: none;
}

button {
  cursor: pointer;
}

#app {
  background: #2c3e50;
  min-height: 100vh;
}

#nav {
  margin: auto;
  width: 960px;
  padding: 30px;
  display: flex;
  justify-content: center;
  a {
    font-weight: bold;
    color: white;
    padding: 2px 3px;
    margin: 0 2px;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
