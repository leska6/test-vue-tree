<template>
    <div>
      <div 
        @click="toggleExpand"
        :style="{'margin-left': `${depth * 20}px`}"
        class="node"
      >
        <span v-if="hasChildren" class="type">
          {{ expanded ? '&#9660;' : '&#9658;' }}
        </span>
        <span @click.stop="selectFolder">{{ node.name }}</span> 
      </div>
  
      <div v-if="expanded">
        <TreeBrowser
          v-for="child in node.children"
          :key="child.id"
          :node="child"
          :depth="depth + 1"
          @select="selectFolder"  
        />
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TreeBrowser',
    props: {
      node: Object,
      depth: {
        type: Number,
        default: 0,
      },
    },
    data() {
      return {
        expanded: false,
      };
    },
    computed: {
      hasChildren() {
        return this.node.children && this.node.children.length > 0;
      },
    },
    methods: {
      toggleExpand() {
        this.expanded = !this.expanded;
      },
      selectFolder() {
        this.$emit('select', this.node.id);
      }
    }
  };
  </script>
  
  <style scoped>
  .node {
    text-align: left;
    font-size: 18px;
    cursor: pointer;
  }
  
  .type {
    cursor: pointer;
  }
  </style>
  