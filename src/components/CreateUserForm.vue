<template>
  <span class="text-gray-700 font-bold text-2xl">Create User</span>
  <div class="flex flex-col gap-3">
    <div class="flex flex-col gap-1">
      <label class="text-gray-700 font-semibold">Nama</label>
      <input
        v-model="inputName"
        class="border-2 py-1 border-gray-400 rounded-md"
      />
    </div>
    <div class="flex flex-col gap-1">
      <label class="text-gray-700 font-semibold">What's on your To Do List</label>
      <input
        v-model="inputCRUD"
        class="border-2 py-1 border-gray-400 rounded-md"
      />
    </div>
    <div class="flex flex-col gap-1">
      <label class="text-gray-700 font-semibold">Date</label>
      <input
        type="datetime-local"
        v-model="inputDate"
        class="border-2 py-1 border-gray-400 rounded-md"
      />
    </div>
    <div class="flex flex-col gap-1">
      <label class="text-gray-700 font-semibold">Category</label>
      <select v-model="inputCategory" class="border-2 py-1 border-gray-400 rounded-md">
        <option value="Low">Low</option>
        <option value="Urgent">Urgent</option>
        <option value="High">High</option>
      </select>
    </div>
  </div>
  <button
    @click="addUser"
    class="px-4 py-2 mt-1 bg-gray-700 w-fit h-fit text-gray-100 font-bold text-sm rounded-xl hover:scale-110 transition-all hover:ease-in-out hover:duration-300"
  >
    Submit
  </button>
</template>

<script>
import { userStore } from "../store/store.js";

export default {
  emits: ["close-modal"],
  data() {
    return {
      userStore,
      inputName: "",
      inputCRUD: "",
      inputDate: "", 
      inputCategory: "Low",
      inputAffairs: "Tasks", 
    };
  },
  methods: {
    addUser() {
      if (
        this.inputNama === "" ||
        this.inputCRUD === "" ||
        this.inputDate === "" ||     
        this.inputCategory === "" ||
        this.inputAffairs === "" 
        )
        return;
      const newUser = {
        id: Date.now().toString(),
        name: this.inputName,
        crud: this.inputCRUD,
        date: this.inputDate, 
        category: this.inputCategory,
      };
      userStore.createUser(newUser);
      this.inputName = "";
      this.inputNrp = "";
      this.inputDate = ""; 
      this.inputCategory = "Low";
      this.$emit("close-modal");
    },
  },
};
</script>


