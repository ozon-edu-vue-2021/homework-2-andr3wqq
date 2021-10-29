<template>
  <div id="app">
    <h2>A JSON Tree View Component in Vue.js</h2>
    <tree-view
        @selected="selectHandler"/>
  </div>
</template>

<script>
import TreeView from './components/TreeView.vue'

export default {
  name: 'App',
  components: {
    TreeView
  },
  data: () => ({
    selectedNode: null
  }),
  methods: {
    selectHandler(node) {
      this.selectedNode = node;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul {
  padding-left: 1em;
  line-height: 1.5em;
  list-style-type: none;
}
</style>
