<template>
<div class="container is-fluid">
  <a href="#/">Home</a> |
  <a href="#/non-existent-path">Broken Link</a>
  <component :is="currentView" />
</div>
</template>

<script>
import Index from './components/Index.vue'
import NotFound from './components/NotFound.vue'
const routes = {
  '/': Index
}
export default {
  name: 'App',
  data() {
    return {
      currentPath: window.location.hash
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
		this.currentPath = window.location.hash
		})
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
