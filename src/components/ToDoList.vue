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
        Add
      </button>
    </div>
    <ul class="w-full mx-5 my-5 text-lg" v-if="todoList.length">
      <li
        v-for="item in todoList"
        :key="item.id"
        class="flex justify-between w-full"
      >
        <p>{{ item.value }}</p>
        <button class="text-red-500" @click="deleteItem(item.id)">
          Delete
        </button>
      </li>
    </ul>
    <p v-else class="text-red-500 my-5">No List Items to display!</p>
  </section>
</template>

<script>
import { onMounted, ref } from "vue";
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
