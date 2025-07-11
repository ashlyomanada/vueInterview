<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";
import Table from "../components/Table.vue";
const TodoLists = ref([]);
const form = ref({ name: "", description: "" });
const editingId = ref(null);

const handleFetch = async () => {
  try {
    const response = await axios.get("http://127.0.0.1:8000/api/todos");
    TodoLists.value = response.data;
  } catch (error) {
    console.error(error);
  }
};

const handleCreate = async () => {
  try {
    if (editingId.value === null) {
      await axios.post("http://127.0.0.1:8000/api/todos", form.value);
      alert("Successfully created");
    } else {
      await axios.put(
        `http://127.0.0.1:8000/api/todos/${editingId.value}`,
        form.value
      );
      alert("Successfully updated");
    }

    await handleFetch();

    form.value.name = "";
    form.value.description = "";
    editingId.value = null;
  } catch (error) {
    console.error(error);
  }
};

const handleEdit = (item) => {
  form.value.name = item.name;
  form.value.description = item.description;
  editingId.value = item.id;
  console.log(item.id);
};

const handleDelete = async (id) => {
  try {
    await axios.delete(`http://127.0.0.1:8000/api/todos/${id}`);
    alert("successfully deleted");
    await handleFetch();
  } catch (error) {
    console.error(error);
  }
};

onMounted(async () => {
  await handleFetch();
});
</script>

<template>
  <div class="flex flex-col">
    <h1>Create Todos</h1>
    <form
      @submit.prevent="handleCreate"
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
        {{ editingId !== null ? "Edit" : "Submit" }}
      </button>
    </form>

    <Table :TodoLists="TodoLists" @edit="handleEdit" @delete="handleDelete" />
  </div>
</template>

<style></style>
