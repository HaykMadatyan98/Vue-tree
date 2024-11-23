<template>
  <div
    class="min-h-screen flex flex-col justify-center items-center bg-gray-100"
  >
    <button
      @click="openModal"
      class="px-6 py-3 bg-blue-500 text-white rounded-lg hover:bg-blue-600"
    >
      Открыть
    </button>

    <CustomModal
      v-if="isModalOpen"
      @close="closeModal"
      @select="selectOnModal"
      title="Выберите папку"
    >
      <FolderTree
        :folders="folders"
        :selectedFolderId="selectedFolderId"
        @select="handleSelect"
      />
    </CustomModal>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import CustomModal from "./components/CustomModal.vue";
import FolderTree from "./components/FolderTree.vue";

const folders = [
  {
    id: 1,
    name: "Папка 1",
    children: [
      { id: 2, name: "Папка 1.1", children: [] },
      {
        id: 3,
        name: "Папка 1.2",
        children: [{ id: 4, name: "Папка 1.2.1", children: [] }],
      },
    ],
  },
  { id: 5, name: "Папка 2", children: [] },
];

const isModalOpen = ref(false);
const selectedFolderId = ref(null);
const openModal = () => (isModalOpen.value = true);
const closeModal = () => (isModalOpen.value = false);

const handleSelect = (id: number) => {
  selectedFolderId.value = id;
};

const selectOnModal = () => {
  console.log("Выбрана папка с ID:", selectedFolderId.value);
  closeModal();
};
</script>
