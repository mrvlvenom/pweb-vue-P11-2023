<template>
  <div class="flex justify-center items-center mt-20">
    <div class="p-4 w-1/2">
      <h2 class="text-2xl font-bold text-gray-700 mb-4 flex items-center">
        <div @click="$router.go(-1)">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="w-6 h-6 mr-4"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M10 19l-7-7m0 0l7-7m-7 7h18"
              class="cursor-pointer"
            />
          </svg>
        </div>
        Edit User
      </h2>
      <div class="flex flex-col gap-4">
        <div class="flex flex-col">
          <label class="text-gray-700 font-semibold">Name</label>
          <input
            v-model="inputNewName"
            class="border rounded-md px-3 py-2 border-gray-400 focus:outline-none focus:border-blue-500"
          />
        </div>
        <div class="flex flex-col">
          <label class="text-gray-700 font-semibold">What's Your To Do List</label>
          <input
            v-model="inputNewNrp"
            class="border rounded-md px-3 py-2 border-gray-400 focus:outline-none focus:border-blue-500"
          />
        </div>
        <div class="flex flex-col">
          <label class="text-gray-700 font-semibold">Date</label>
          <input
            type="datetime-local"
            v-model="inputNewDate"
            class="border rounded-md px-3 py-2 border-gray-400 focus:outline-none focus:border-blue-500"
          />
        </div>
        <div class="flex flex-col">
          <label class="text-gray-700 font-semibold">Category</label>
          <select
            v-model="inputNewCategory"
            class="border rounded-md px-3 py-2 border-gray-400 focus:outline-none focus:border-blue-500"
          >
            <option value="Low">Low</option>
            <option value="High">High</option>
            <option value="Urgent">Urgent</option>
          </select>
        </div>
      </div>
      <button
        @click="updateUser"
        class="px-4 py-2 mt-4 bg-gray-700 text-gray-100 font-bold text-sm rounded-lg hover:bg-gray-800 transition duration-300 ease-in-out transform hover:scale-105 focus:outline-none"
      >
        Submit
      </button>
    </div>
  </div>
</template>

<script>
import { userStore } from "../store/store.js";

export default {
  data() {
    return {
      userStore,
      id: this.$route.params.id,
      inputNewName: "",
      inputNewNrp: "",
      inputNewDate: "", 
      inputNewCategory: "Low", 
    };
  },
  methods: {
    getUserById() {
      const user = this.userStore.users.find((user) => user.id === parseInt(this.id) || user.id === this.id);
      if (user) {
        this.inputNewName = user.name;
        this.inputNewNrp = user.nrp;
        this.inputNewDate = user.date || ""; 
        this.inputNewCategory = user.category || "Low"; 
      }
    },
    updateUser() {
      const updatedUser = {
        id: this.id,
        name: this.inputNewName,
        nrp: this.inputNewNrp,
        date: this.inputNewDate, 
        category: this.inputNewCategory,
      };
      userStore.editUser(updatedUser);
      this.$router.push("/");
    },
  },
  mounted() {
    this.getUserById();
  },
};
</script>
