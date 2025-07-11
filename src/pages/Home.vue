<!-- Parent Component  -->
<script setup>
import { ref, computed } from "vue";
import UserCard from "../components/UserCard.vue";

const allColleagues = ref([
  { name: "Joseph", age: 26 },
  { name: "Daniel", age: 38 },
  { name: "Joshua", age: 50 },
  { name: "Yuri", age: 42 },
  { name: "Rose", age: 25 },
  { name: "Maria", age: 29 },
  { name: "Mark", age: 40 },
  { name: "Pauline", age: 38 },
  { name: "Jasmine", age: 38 },
  { name: "Angel", age: 39 },
]);

const selectedColleagues = ref([]);

const availableColleagues = computed(() =>
  allColleagues.value.filter(
    (c) => !selectedColleagues.value.find((sel) => sel.name === c.name)
  )
);

const addColleague = (user) => {
  if (!selectedColleagues.value.find((u) => u.name === user.name)) {
    selectedColleagues.value.push(user);
  }
};
</script>

<template>
  <div class="p-6">
    <h1 class="text-2xl font-bold mb-4">Available Colleagues</h1>
    <transition-group
      name="fade"
      tag="div"
      class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-4"
    >
      <UserCard
        v-for="user in availableColleagues"
        :key="user.name"
        :user="user"
        @add="addColleague(user)"
      />
    </transition-group>

    <h1 class="text-2xl font-bold mt-8 mb-4">Selected Colleagues</h1>
    <transition-group
      name="slide"
      tag="div"
      class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-4"
    >
      <UserCard
        v-for="user in selectedColleagues"
        :key="user.name"
        :user="user"
        selected
      />
    </transition-group>
  </div>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: all 0.4s ease;
}
.slide-enter-from {
  transform: translateY(10px);
  opacity: 0;
}
.slide-leave-to {
  transform: translateY(-10px);
  opacity: 0;
}
</style>
