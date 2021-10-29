<template>
  <div class="tree-view--wrapper">
    <ul>
      <tree-view-item
          :item="treeData"
          @selected="selectHandler"
      ></tree-view-item>
    </ul>
  </div>
</template>

<script lang="ts">
import TreeViewItem from './TreeViewItem.vue';
import json from '../../public/static/node_modules.json';

export default {
  name: 'TreeView',
  components: { TreeViewItem },
  data: () => ({
    treeData: json,
  }),
  methods: {
    selectHandler(node) {
      this.$emit('selected', node);
    },
  }
};
</script>

<style scoped>
.tree-view--wrapper {
  display: block;
  text-align: left;
}
</style>