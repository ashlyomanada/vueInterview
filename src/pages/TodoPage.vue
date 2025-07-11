<script setup>
import { ref } from "vue";
import TodoList from "../components/TodoList.vue";

const TodoLists = ref([]);
const form = ref({ name: "", description: "" });
const editingIndex = ref(null);

const handleAddLists = () => {
  if (form.value.name && form.value.description) {
    if (editingIndex.value === null) {
      TodoLists.value.push({ ...form.value });
    } else {
      TodoLists.value[editingIndex.value] = { ...form.value };
    }

    form.value.name = "";
    form.value.description = "";
    editingIndex.value = null;

    console.log(TodoLists.value);
  }
};

const handleEdit = (item) => {
  form.value.name = item.name;
  form.value.description = item.description;
  editingIndex.value = item.index;
};

const handleDelete = (index) => {
  TodoLists.value.splice(index, 1);
};
</script>

<template>
  <div class="flex flex-col px-20">
    <form
      @submit.prevent="handleAddLists"
      class="flex flex-col justify-center max-w-lg mx-auto px-4 space-y-8 py-22"
    >
      <div>
        <label class="mb-2 text-slate-900 font-medium text-base block"
          >Name</label
        >
        <input
          type="text"
          placeholder="Name"
          v-model="form.name"
          class="px-4 py-2 text-base rounded-md bg-white border border-gray-400 w-full outline-blue-500"
        />
      </div>
      <div>
        <label class="mb-2 text-slate-900 font-medium text-base block"
          >Description</label
        >
        <input
          type="text"
          placeholder="Description"
          v-model="form.description"
          class="px-4 py-2 text-base rounded-md bg-white border border-gray-400 w-full outline-blue-500"
        />
      </div>

      <button
        type="submit"
        class="px-5 py-2.5 rounded-lg cursor-pointer text-white text-sm tracking-wider font-medium border border-current outline-none bg-blue-700 hover:bg-blue-800 active:bg-blue-700"
      >
        {{ editingIndex !== null ? "Edit" : "Submit" }}
      </button>
    </form>

    <TodoList
      :TodoLists="TodoLists"
      @edit="handleEdit"
      @delete="handleDelete"
    />
  </div>
</template>

<style></style>
