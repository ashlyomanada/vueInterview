<script setup>
const props = defineProps({
  TodoLists: Array,
});

const emits = defineEmits(["edit"], ["delete"]);
</script>
<template>
  <div class="overflow-x-auto">
    <table class="min-w-full divide-y divide-gray-200">
      <thead class="bg-gray-100 whitespace-nowrap">
        <tr>
          <th
            class="px-4 py-4 text-left text-xs font-semibold text-slate-900 uppercase tracking-wider"
          >
            Id
          </th>
          <th
            class="px-4 py-4 text-left text-xs font-semibold text-slate-900 uppercase tracking-wider"
          >
            Name
          </th>
          <th
            class="px-4 py-4 text-left text-xs font-semibold text-slate-900 uppercase tracking-wider"
          >
            Description
          </th>

          <th
            class="px-4 py-4 text-left text-xs font-semibold text-slate-900 uppercase tracking-wider"
          >
            Actions
          </th>
        </tr>
      </thead>

      <tbody
        class="bg-white divide-y divide-gray-200 whitespace-nowrap"
        v-if="TodoLists.length"
      >
        <tr v-for="(list, index) in TodoLists" :key="list.name">
          <td class="px-4 py-4 text-sm text-slate-900 font-medium">
            {{ index + 1 }}
          </td>
          <td class="px-4 py-4 text-sm text-slate-900 font-medium">
            {{ list.name }}
          </td>
          <td class="px-4 py-4 text-sm text-slate-600 font-medium">
            {{ list.description }}
          </td>

          <td class="px-4 py-4 text-sm">
            <button
              class="cursor-pointer text-blue-600 font-medium mr-4"
              @click="emits('edit', { ...list, index })"
            >
              Edit
            </button>
            <button
              class="cursor-pointer text-red-600 font-medium"
              @click="emits('delete', index)"
            >
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
