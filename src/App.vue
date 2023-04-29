<template>
  <div id="app" :class="changeBackground? 'bg-green-500':'bg-[#8a2be2]'">
    <to-do-list @getCheckedItems="getCheckedItems"/>
  </div>
</template>

<script>
import { ref } from "vue";
import ToDoList from './components/ToDoList.vue'
export default {
  name: 'App',
  components: {
    ToDoList
  },
  setup(){
    const changeBackground = ref(false);
    const getCheckedItems = (checked) => {
      if(checked){
        changeBackground.value = true;
      }
      else {
        changeBackground.value = false;
      }
    } 

    return {
      getCheckedItems,
      changeBackground,
    }
  },
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  height: 100vh;
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
