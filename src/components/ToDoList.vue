<template>
  <section class="bg-white h-[600px] w-[500px] m-10 rounded-[20px] flex flex-col items-center p-5">
    <h1 class="my-5 text-3xl font-bold">To Do List</h1>
    <div class="bg-gray-100 w-full [400px] flex p-2 rounded-xl shadow-md">
      <input class="bg-gray-100 p-1 w-full" @keydown.enter="addItem" type="text" v-model="newItem" maxlength="40" />
      <button class="px-5 text-[#8a2be2]" @click="addItem">
        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" viewBox="0 0 128 128"
          style="enable-background:new 0 0 128 128" xml:space="preserve">
          <path style="fill:#8a2be2"
            d="M128 63.954c0 2.006-.797 3.821-2.136 5.127-1.308 1.337-3.125 2.133-5.166 2.133H71.302v49.356c0 4.012-3.284 7.292-7.302 7.292-2.009 0-3.827-.828-5.166-2.134-1.308-1.337-2.136-3.152-2.136-5.159V71.214H7.302c-4.05 0-7.302-3.248-7.302-7.26 0-2.006.797-3.853 2.136-5.159a7.279 7.279 0 0 1 5.166-2.134h49.395V7.306c0-4.012 3.284-7.26 7.302-7.26 2.009 0 3.827.828 5.166 2.133a7.238 7.238 0 0 1 2.136 5.127v49.356h49.395A7.276 7.276 0 0 1 128 63.954z" />
        </svg>
      </button>
    </div>
    <div class="w-full mt-2">
      <span class="text-red-500 text-left">Total characters remaining {{ displayRemainingCharacters }}</span>
    </div>
    <div class="w-full flex justify-end">
      <div class="bg-gray-100 px-3 py-2 rounded-lg my-3">
          <label for="sort">Sort:</label>
          <select class="bg-gray-100" name="sort" id="sort" v-model="sort" @change="sortedList">
            <option value="default">Select</option>
            <option value="alphabetically">Alphabetically</option>
          <option value="time">Time</option>
        </select>
      </div>
    </div>
    <ul class="w-full mx-5 my-5 text-lg h-full overflow-y-scroll" v-if="todoList.length">
      <li v-for="(item, index) in todoList" :key="item.id" class="flex justify-between items-center w-full my-2"
        @click="itemChecked(item.isChecked, index)">
        <label class="flex w-full items-center gap-2 m-2 bg-gray-50 rounded-xl px-3 pb-1 shadow-md">
          <svg v-if="item.isChecked" class="h-10 w-10 text-green-500" viewBox="0 0 24 24"
            version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
            <!-- Uploaded to: SVG Repo, www.svgrepo.com, Generator: SVG Repo Mixer Tools -->
            <title>ic_fluent_checkbox_checked_24_filled</title>
            <desc>Created with Sketch.</desc>
            <g id="🔍-Product-Icons" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
              <g id="ic_fluent_checkbox_checked_24_filled" fill="currentColor" fill-rule="nonzero">
                <path
                  d="M18,3 C19.6568542,3 21,4.34314575 21,6 L21,18 C21,19.6568542 19.6568542,21 18,21 L6,21 C4.34314575,21 3,19.6568542 3,18 L3,6 C3,4.34314575 4.34314575,3 6,3 L18,3 Z M16.4696699,7.96966991 L10,14.4393398 L7.53033009,11.9696699 C7.23743687,11.6767767 6.76256313,11.6767767 6.46966991,11.9696699 C6.1767767,12.2625631 6.1767767,12.7374369 6.46966991,13.0303301 L9.46966991,16.0303301 C9.76256313,16.3232233 10.2374369,16.3232233 10.5303301,16.0303301 L17.5303301,9.03033009 C17.8232233,8.73743687 17.8232233,8.26256313 17.5303301,7.96966991 C17.2374369,7.6767767 16.7625631,7.6767767 16.4696699,7.96966991 Z"
                  id="🎨-Color">

                </path>
              </g>
            </g>
          </svg>
          <svg v-else class="h-10 w-10 text-[#8a2be2]" viewBox="0 0 24 24" version="1.1"
            xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
            <!-- Uploaded to: SVG Repo, www.svgrepo.com, Generator: SVG Repo Mixer Tools -->
            <title>ic_fluent_checkbox_unchecked_24_regular</title>
            <desc>Created with Sketch.</desc>
            <g id="🔍-Product-Icons" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
              <g id="ic_fluent_checkbox_unchecked_24_regular" fill="currentColor" fill-rule="nonzero">
                <path
                  d="M5.75,3 L18.25,3 C19.7687831,3 21,4.23121694 21,5.75 L21,18.25 C21,19.7687831 19.7687831,21 18.25,21 L5.75,21 C4.23121694,21 3,19.7687831 3,18.25 L3,5.75 C3,4.23121694 4.23121694,3 5.75,3 Z M5.75,4.5 C5.05964406,4.5 4.5,5.05964406 4.5,5.75 L4.5,18.25 C4.5,18.9403559 5.05964406,19.5 5.75,19.5 L18.25,19.5 C18.9403559,19.5 19.5,18.9403559 19.5,18.25 L19.5,5.75 C19.5,5.05964406 18.9403559,4.5 18.25,4.5 L5.75,4.5 Z"
                  id="🎨Color">

                </path>
              </g>
            </g>
          </svg>
          <!--           <input v-model="item.isChecked" type="checkbox" class="w-[20px] h-[20px]"> -->
          <div class="w-full">
            <p class="font-bold text-2xl break-all overflow-wrap" :class="item.isChecked ? 'line-through' : ''">{{
              item.value
            }}</p>
            <p class="text-xs text-gray-500">{{ getDate(item.dateTime) }}</p>
          </div>
        </label>
        <button class="text-red-500" @click="deleteItem(item.id)">
          <svg class="w-9 h-9" data-name="Layer 3" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 128 128">
            <path style="fill:#FF0000"
              d="M64 21.433A42.567 42.567 0 1 0 106.567 64 42.615 42.615 0 0 0 64 21.433zm0 80.912A38.345 38.345 0 1 1 102.345 64 38.389 38.389 0 0 1 64 102.345z" />
            <path style="fill:#FF0000"
              d="M79.459 48.3a2.11 2.11 0 0 0-2.985 0L64 60.778 51.523 48.3a2.111 2.111 0 1 0-2.985 2.985l12.476 12.478-12.473 12.474a2.111 2.111 0 1 0 2.985 2.985L64 66.748l12.474 12.474a2.111 2.111 0 0 0 2.985-2.985L66.984 63.763l12.475-12.477a2.11 2.11 0 0 0 0-2.986z" />
          </svg>
        </button>
      </li>
    </ul>
    <p v-else class="text-red-500 my-5">No List Items to display!</p>
    <p v-if="getCheckedItems !== todoList.length" class="text-red-500">Completed: {{ getCheckedItems }}/{{ todoList.length
    }}</p>
    <p v-else-if="todoList.length > 0" class="text-green-500">All Tasks Completed!</p>
  </section>
</template>

<script>
import { computed, onMounted, ref, watch } from "vue";
import moment from 'moment';

export default {
  name: "ToDoList",
  setup(props, context) {
    const newItem = ref("");
    const todoList = ref([]);
    const sort = ref("default");
    const displayRemainingCharacters = ref(40);
    let counter = 0;
    //let index = todoList?.value?.length? todoList?.value[todoList?.value?.length - 1]?.id + 1 : 0;

    const addItem = () => {
      if (newItem.value.trim() !== "") {
        const itemIndex = todoList.value.findIndex(
          (item) => item.value === newItem.value.trim()
        );

        if (itemIndex === -1) {
          const item = {
            id: counter,
            value: newItem.value,
            isChecked: false,
            dateTime: moment(),
          };
          todoList.value.push(item);
          localStorage.setItem('todoList', JSON.stringify(todoList.value));
          localStorage.setItem('counter', ++counter);
          newItem.value = "";
          sortedList();
        }
        displayRemainingCharacters.value = 40;
      }
    };

    watch(newItem, (newValue) => {
      displayRemainingCharacters.value = 40 - newValue.length;
    })

    const getDate = (dateTime) => {
      const now = moment();
      const date = moment(dateTime);
      const isToday = now.isSame(date, 'day');
      const isYesterday = now.clone().subtract(1, 'day').isSame(date, 'day');
      if (isToday) {
        return `Today ${date.format('hh:mm A')}`;
      } else if (isYesterday) {
        return `Yesterday ${date.format('hh:mm A')}`;
      } else {
        return date.format('DD MMMM, YYYY, hh:mm A');
      }
    }

    const getCheckedItems = computed(() => {
      let count = 0;
      todoList.value.forEach((item) => {
        if (item.isChecked) count++;
      });

      if(todoList.value.length > 0 && todoList.value.length === count) {
        context.emit('getCheckedItems', true)
      }
      else {
        context.emit('getCheckedItems', false);
      }
      return count;
    });

    const deleteItem = (id) => {
      const index = todoList.value.findIndex((item) => item.id === id);
      todoList.value.splice(index, 1);
      localStorage.setItem('todoList', JSON.stringify(todoList.value));
    };

    const itemChecked = (value, index) => {
      todoList.value[index].isChecked = !value;
      localStorage.setItem('todoList', JSON.stringify(todoList.value));
    }

    const sortedList = () => {
      if (sort.value === 'alphabetically') {
        todoList.value.sort((a, b) => a.value.localeCompare(b.value));
      }
      else if (sort.value === 'time') {
        todoList.value.sort((a, b) => {
          return b.dateTime - a.dateTime;
        })
      }
      else if (sort.value === 'default') {
        todoList.value.sort((a, b) => a.id - b.id);
      }
    };

    onMounted(() => {
      const storedData = localStorage.getItem('todoList');
      counter = localStorage.getItem('counter');
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
      getCheckedItems,
      sort,
      sortedList,
      getDate,
      displayRemainingCharacters,
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
}</style>
