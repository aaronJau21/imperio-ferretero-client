<template>
  <!-- component -->
  <div class="h-screen md:flex">
    <div
      class="relative overflow-hidden md:flex w-1/2 bg-gradient-to-tr from-primary to-secundary i justify-around items-center hidden"
    >
      <div>
        <h1 class="text-white font-bold text-4xl font-sans">Delta Construye</h1>
        <p class="text-white mt-1">Tu Ferreteria de confianza</p>
      </div>
      <div
        class="absolute -bottom-32 -left-40 w-80 h-80 border-4 rounded-full border-opacity-30 border-t-8"
      ></div>
      <div
        class="absolute -bottom-40 -left-20 w-80 h-80 border-4 rounded-full border-opacity-30 border-t-8"
      ></div>
      <div
        class="absolute -top-40 -right-0 w-80 h-80 border-4 rounded-full border-opacity-30 border-t-8"
      ></div>
      <div
        class="absolute -top-20 -right-20 w-80 h-80 border-4 rounded-full border-opacity-30 border-t-8"
      ></div>
    </div>
    <div class="flex md:w-1/2 justify-center py-10 items-center bg-white">
      <RegisterForm />
    </div>
  </div>
</template>

<script setup lang="ts">
import RegisterForm from "~/components/auth/register/RegisterForm.vue";

definePageMeta({
  layout: "auth",
});
useHead({
  title: "Register",
  meta: [
    {
      name: "description",
      content: "Registro de Delta construye",
    },
  ],
});
</script>

<style scoped></style>
