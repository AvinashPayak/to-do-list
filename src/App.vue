<template>
  <div id="app">
    <to-do-list/>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList.vue'
export default {
  name: 'App',
  components: {
    ToDoList
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  height: 100vh;
  background-color: #8a2be2;
  display: flex;
  justify-content: center;
}

.btn {
  @apply rounded-lg px-4 py-2
}

.btn-primary {
  background-color: orange;
  color: white;
}
</style>
