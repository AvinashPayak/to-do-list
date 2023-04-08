<template>
  <section
    class="bg-white h-[600px] w-[500px] m-10 rounded-[20px] flex flex-col items-center p-5"
  >
    <h1 class="my-5 text-3xl font-bold">To Do List</h1>
    <div class="bg-gray-100 w-full [400px] flex p-2 rounded-xl">
      <input class="bg-gray-100 p-1 w-full" @keydown.enter="addItem" type="text" v-model="newItem" />
      <button
        class="px-5 text-[#8a2be2]"
        @click="addItem"
      >
      <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" viewBox="0 0 128 128" style="enable-background:new 0 0 128 128" xml:space="preserve"><path style="fill:#8a2be2" d="M128 63.954c0 2.006-.797 3.821-2.136 5.127-1.308 1.337-3.125 2.133-5.166 2.133H71.302v49.356c0 4.012-3.284 7.292-7.302 7.292-2.009 0-3.827-.828-5.166-2.134-1.308-1.337-2.136-3.152-2.136-5.159V71.214H7.302c-4.05 0-7.302-3.248-7.302-7.26 0-2.006.797-3.853 2.136-5.159a7.279 7.279 0 0 1 5.166-2.134h49.395V7.306c0-4.012 3.284-7.26 7.302-7.26 2.009 0 3.827.828 5.166 2.133a7.238 7.238 0 0 1 2.136 5.127v49.356h49.395A7.276 7.276 0 0 1 128 63.954z"/></svg>
      </button>
    </div>
    <ul class="w-full mx-5 my-5 text-lg" v-if="todoList.length">
      <li
        v-for="(item, index) in todoList"
        :key="item.id"
        class="flex justify-between items-center w-full"
      >
        <label class="flex items-center gap-2">
          <input @click="itemChecked(item.isChecked, index)" v-model="item.isChecked" type="checkbox" class="w-5 h-5">
          <p :class="item.isChecked? 'line-through':''">{{ item.value }}</p>
        </label>
        <button class="text-red-500" @click="deleteItem(item.id)">
          <svg class="w-9 h-9" data-name="Layer 3" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 128 128">
            <path style="fill:#FF0000" d="M64 21.433A42.567 42.567 0 1 0 106.567 64 42.615 42.615 0 0 0 64 21.433zm0 80.912A38.345 38.345 0 1 1 102.345 64 38.389 38.389 0 0 1 64 102.345z"/>
            <path style="fill:#FF0000" d="M79.459 48.3a2.11 2.11 0 0 0-2.985 0L64 60.778 51.523 48.3a2.111 2.111 0 1 0-2.985 2.985l12.476 12.478-12.473 12.474a2.111 2.111 0 1 0 2.985 2.985L64 66.748l12.474 12.474a2.111 2.111 0 0 0 2.985-2.985L66.984 63.763l12.475-12.477a2.11 2.11 0 0 0 0-2.986z"/>
          </svg>
        </button>
      </li>
    </ul>
    <p v-else class="text-red-500 my-5">No List Items to display!</p>
  </section>
</template>

<script>
import { onMounted, ref} from "vue";
export default {
  name: "ToDoList",
  setup() {
    const newItem = ref("");
    const todoList = ref([]);

    const addItem = () => {
      if (newItem.value.trim() !== "") {
        const itemIndex = todoList.value.findIndex(
          (item) => item.value === newItem.value.trim()
        );

        if (itemIndex === -1) {
          const id = todoList.value.length + 1;
          const item = { id, value: newItem.value };
          todoList.value.push(item);
          localStorage.setItem('todoList', JSON.stringify(todoList.value));
          newItem.value = "";
        }
      }
    };

    const deleteItem = (id) => {
      const index = todoList.value.findIndex((item) => item.id === id);
      todoList.value.splice(index, 1);
      localStorage.setItem('todoList', JSON.stringify(todoList.value));
    };

    const itemChecked = (value, index) => {
      todoList.value[index].isChecked = !value;
      localStorage.setItem('todoList', JSON.stringify(todoList.value));
    }

    onMounted(()=>{
        const storedData = localStorage.getItem('todoList');
      if (storedData) {
        todoList.value = JSON.parse(storedData);
      }
    });

    return {
      newItem,
      todoList,
      addItem,
      deleteItem,
      itemChecked,
    };
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

input:focus {
  outline: none;
}
</style>
