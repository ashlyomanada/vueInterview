<!-- Child Component -->
<script setup>
import { computed } from "vue";

const props = defineProps({
  user: Object,
  selected: Boolean,
});

const emit = defineEmits(["add"]);

const handleClick = () => {
  if (!props.selected) emit("add");
};

const ageColor = computed(() => {
  if (props.user.age < 30) return "green";
  if (props.user.age < 40) return "orange";
  return "red";
});
</script>

<template>
  <div
    class="border rounded p-4 shadow hover:bg-gray-50 transition cursor-pointer"
    :class="{ 'bg-green-100': selected }"
    @click="handleClick"
  >
    <p class="font-semibold text-lg">{{ user.name }}</p>
    <p :style="{ color: ageColor }">Age: {{ user.age }}</p>
  </div>
</template>
