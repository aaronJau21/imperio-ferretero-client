<template>
  <header class="py-5 bg-white flex flex-col gap-5">
    <!-- Header Options -->
    <div class="md:flex md:justify-between mx-9 items-center hidden ">
      <img src="/logo.jpg" alt="Logo de Imperio Ferretero" class="w-40" />
      <div class="flex bg-white border border-gray-400 rounded">
        <input
          placeholder="Buscar Productos"
          class="w-96 p-2 border-none outline-none rounded-l"
        />
        <button
          class="flex items-center bg-primary px-3 py-2 text-white rounded-r hover:bg-red-500 transition-colors"
          aria-label="Buscar productos"
        >
          <Icon name="weui:search-filled" />
          <span class="ml-2">Buscar</span>
        </button>
      </div>
      <div class="flex items-center gap-x-5">
        <Icon
          name="material-symbols:shopping-cart-outline"
          size="31"
          class="cursor-pointer transition-transform transform hover:scale-110 text-gray-700 hover:text-primary"
        />
        <NuxtLink to="/auth/login" class="flex items-center">
          <Icon
            name="material-symbols:account-circle-full"
            size="31"
            class="cursor-pointer transition-transform transform hover:scale-110 text-gray-700 hover:text-primary"
          />
        </NuxtLink>
      </div>
    </div>

    <!-- Dropdown Search Results -->
    <div class="absolute bg-white w-[85%] z-10">
      <ItemRouteResponseComponent />
    </div>

    <!-- Header Mobile -->
    <div class="flex justify-between items-center px-3 md:hidden">
      <img src="/delta-logo.png" alt="Logo de Imperio Ferretero" class="w-32" />
      <div class="flex justify-between gap-x-5">
        <Icon
          name="material-symbols:shopping-cart-outline"
          size="25"
          class="cursor-pointer"
        />
        <Icon
          name="heroicons-outline:bars-3"
          size="25"
          class="cursor-pointer"
          @click="showModal.showModal()"
        />
        <Icon
          name="material-symbols:account-circle-full"
          size="25"
          class="cursor-pointer"
        />
      </div>
    </div>

    <!-- Navigation Routes -->
    <ItemsRoutesComponent />
  </header>
</template>

<script setup lang="ts">
import { NuxtLink } from "#components";
import ItemRouteResponseComponent from "./ItemRouteResponseComponent.vue";
import ItemsRoutesComponent from "./ItemsRoutesComponent.vue";
import { useShowModalStore } from "~/store/ui/showModal.store";

const showModal = useShowModalStore();
</script>

<style scoped>
input::placeholder {
  color: #9ca3af;
}


</style>
