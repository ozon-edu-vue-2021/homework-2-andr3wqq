<template>
  <li>
    <span
        :class="['tree-view--item', { 'bold': isFolder, 'link': isLink }]"
        @click="toggleHandler">
      <span v-if="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
      {{ item.name }}
    </span>
    <ul v-show="isOpen" v-if="isFolder">
      <tree-view-item
          class="tree-view--item"
          v-for="(child, index) in item.contents"
          :key="index"
          :item="child"
      ></tree-view-item>
    </ul>
  </li>
</template>

<script lang="ts">
/*
type File = {
  type: 'file',
  name: string,
};

type Link = {
  type: 'link',
  name: string,
  target: string,
};

type Directory = {
  type: 'directory',
  name: string,
  contents: Item[],
};

type Item = Directory | File | Link;
*/

export default {
  name: "TreeViewItem",
  props: {
    item: Object
  },
  data: () => ({
    isOpen: false
  }),
  computed: {
    isFolder: function () {
      return this.item.type === 'directory' && this.item.contents.length;
    },
    isLink: function () {
      return this.item.type === 'link';
    },
  },
  methods: {
    toggleHandler: function () {
      if (this.isFolder) {
        this.isOpen = !this.isOpen;
      }
    },
  }
};
</script>

<style>
.tree-view--item {
  cursor: pointer;
}

.bold {
  font-weight: bold;
}

.link {
  color: green;
  text-decoration: underline;
}

.selected {
  color: blue;
}
</style>