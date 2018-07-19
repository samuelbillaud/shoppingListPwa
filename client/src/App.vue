<template>
  <div id="app">
    <header>
      <div>
        <span>Vue.js PWA</span>
      </div>
    </header>
    <main>
      <img src="./assets/logo.png" alt="Vue.js PWA">
      <router-view></router-view>
      <vue-progress-bar></vue-progress-bar>
    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  mounted() {
    // TODO: Supprimer setTimeout à la fin du dev
    setTimeout(() => this.$Progress.finish(), 3000)
  },
  created() {
    this.$Progress.start()
    this.$router.beforeEach((to, from, next) => {
      if (to.meta.progress !== undefined) {
        let meta = to.meta.progress
        this.$Progress.parseMeta(meta)
      }
      this.$Progress.start()
      next()
    })
    this.$router.afterEach((to, from) => {
      this.$Progress.finish()
    })
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

main {
  text-align: center;
  margin-top: 76px;
}

header {
  position: fixed;
  top: 1px;
  width: 100%;
  margin: 0;
  background-color: #fff;
  color: #42b983;
}

header div {
  width: 90%;
  height: 56px;
  margin: auto;
  border-bottom: 1px solid #ededed;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: 0.02em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 16px;
}
</style>
