<template>
  <div>
    <button @click="openModal">Открыть</button>

    <div v-if="isModalOpen" class="modal-overlay" @click="closeModal">
      <div class="modal-content" @click.stop>
        <h3>Дерево папок</h3>
        <TreeBrowser :node="root" @select="handleFolderSelect"/>
        
      
        <button @click="confirmSelection">Ок</button>
        <button @click="closeModal">Закрыть</button>
      </div>
    </div>

    <div id="app">
    </div>
  </div>
</template>

<script>
import TreeBrowser from './components/TreeBrowser.vue';

export default {
  name: 'App',
  data() {
    return {
      isModalOpen: false,  
      selectedFolderId: null,  
      
      root: {
        id: 1,
        name: 'Папка 1',
        children: [
          {
            id: 2,
            name: 'Папка 1.1',
            children: []  
          },
          {
            id: 3,
            name: 'Папка 1.2',
            children: [
              {
                id: 4,
                name: 'Папка 1.2.1',
                children: []  
              }
            ]
          },
          {
            id: 5,
            name: 'Папка 2',
            children: []  
          }
        ]
      }
    };
  },
  components: {
    TreeBrowser
  },
  methods: {
    openModal() {
      this.isModalOpen = true; 
    },
    closeModal() {
      this.isModalOpen = false; 
    },
    handleFolderSelect(folderId) {
      this.selectedFolderId = folderId;
      console.log(`Выбрана папка с ID: ${folderId}`); 
    },
    confirmSelection() {
      this.$emit('select', this.selectedFolderId);
      this.closeModal();
    }
  }
};
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

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  width: 400px;
  text-align: center;
}

button {
  background-color: #90e641;
  width: 150px;
  height: 40px;
  color: rgb(0, 0, 0);
  font-size: 14px;
  border-radius: 16px;
  margin-top: 50px;
}
</style>
