<template>
  <li class="tree-view--item">
    <input type="radio" name="radio" :id="itemId" :value="item.name">
    <label :class="{ 'bold': isFolder, 'link': isLink }"
           :for="itemId"
           @click="toggleHandler"
           key="label">
      <span v-if="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
      {{ item.name }}
    </label>
    <ul v-show="isOpen" v-if="isFolder">
      <tree-view-item
          class="tree-view--item"
          v-for="(child, index) in item.contents"
          :key="index"
          :item="child"
          @selected="selectHandler"
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
    item: {
      type: Object,
      required: true
    },
  },
  data: () => ({
    isOpen: false,
    isSelected: false,
    itemId: ''
  }),
  computed: {
    isFolder() {
      return this.item.type === 'directory' && this.item.contents.length;
    },
    isLink() {
      return this.item.type === 'link';
    },
  },
  methods: {
    selectHandler(node) {
      this.isSelected = null;
      this.isSelected = this.itemId;
      this.$emit('selected', node);
    },
    toggleHandler() {
      if (this.isFolder) {
        this.isOpen = !this.isOpen;
      }
      this.selectHandler(this);
    },
  },
  created() {
    this.itemId = `${this.item.name}_${this.item.type}_${this._uid}`;
  }
};
</script>

<style scoped>
ul .tree-view--item :hover:before {
  background: rgba(190, 235, 255, 0.3);
}

ul .tree-view--item input[type='radio'] {
  display: none;
}

ul .tree-view--item input[type='radio']:checked + label:before {
  background: rgba(83, 215, 220, 0.3);
}

ul label {
  cursor: pointer;
  user-select: none;
}

ul label:before {
  box-sizing: border-box;
  content: '';
  height: 21px;
  left: 0;
  position: absolute;
  right: 0;
}

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
</style>