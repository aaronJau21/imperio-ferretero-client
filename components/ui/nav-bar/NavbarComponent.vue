<template>
  <header class="p-2 bg-white flex flex-col gap-5 relative">
    <!-- Dropdown Search Results -->
    <div class="absolute bg-white w-[85%] z-10">
      <ItemRouteResponseComponent />
    </div>

    <!-- Header Mobile -->
    <div class="flex justify-between items-center gap-2">
      <NuxtLink to="/">
        <img src="/logo.png" alt="Logo de Imperio Ferretero" class="w-48" />
      </NuxtLink>
      <div
        class="w-[35rem] bg-white border border-gray-400 rounded hidden md:block"
      >
        <div class="flex">
          <input
            v-model="searchQuery"
            placeholder="Buscar"
            class="w-[35rem] p-2 border-none outline-none rounded-l"
          />
          <button
            class="flex items-center bg-primary px-3 py-2 text-white rounded-r hover:bg-red-500 transition-colors"
            aria-label="Buscar"
            @click="handleSearch"
          >
            <Icon name="weui:search-filled" />
            <span class="ml-2">Buscar</span>
          </button>
        </div>
      </div>
      <div class="flex justify-between gap-x-5">
        <Icon
          name="material-symbols:shopping-cart-outline"
          size="25"
          class="cursor-pointer transition-transform active:scale-90 active:opacity-70"
          @click="isCartModalOpen = true"
        />
        <Icon
          name="heroicons-outline:bars-3"
          size="25"
          class="cursor-pointer block md:hidden transition-transform active:scale-90 active:opacity-70"
          @click="showModal.showModal()"
        />
        <div v-if="user">
          <button
            @click="showModalSearch = !showModalSearch"
            class="flex items-center gap-2 bg-gray-300 rounded-full px-3 py-1"
          >
            <p class="text-xl">{{ getUser?.name?.[0] }}</p>
          </button>
          <CardInfoHistoryPayload
            :getUser="getUser"
            :showModalSearch="showModalSearch"
          />
        </div>
        <div v-else>
          <NuxtLink to="/auth/login">
            <Icon
              name="material-symbols:account-circle-full"
              size="25"
              class="cursor-pointer transition-transform active:scale-90 active:opacity-70"
            />
          </NuxtLink>
        </div>
      </div>
    </div>

    <!-- Navigation Routes -->
    <ItemsRoutesComponent />

    <!-- Cart Modal -->
    <CartModal :isOpen="isCartModalOpen" @close="isCartModalOpen = false" />
  </header>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { NuxtLink } from "#components";
import ItemRouteResponseComponent from "./ItemRouteResponseComponent.vue";
import ItemsRoutesComponent from "./ItemsRoutesComponent.vue";
import CartModal from "./CartModal.vue";
import { useShowModalStore } from "~/store/ui/showModal.store";
import type { IUser } from "~/interfaces";
import CardInfoHistoryPayload from "./CardInfoHistoryPayload.vue";

const showModal = useShowModalStore();
const isCartModalOpen = ref(false);
const user = useCookie<IUser>("user");
const config = useRuntimeConfig();
const getUser = ref<IUser | null>(null);
const searchQuery = ref("");
const showDropdown = ref(false);
const showModalSearch = ref(false);

const handleSearch = () => {
  // Lógica de búsqueda aquí
  showDropdown.value = true; // Mostrar dropdown si hay resultados
};

onMounted(async () => {
  if (user.value) {
    const { data } = await useFetch<IUser>(
      `${config.public.api_url}/client/getClient/${user.value.name}`
    );
    getUser.value = data.value;
  }
});
</script>

<style scoped>
input::placeholder {
  color: #9ca3af;
}
</style>
