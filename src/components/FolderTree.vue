<template>
  <div>
    <ul>
      <li v-for="folder in folders" :key="folder.id">
        <div @click="onSelect(folder.id)">
          <span :class="{ selected: selectedFolderId === folder.id }">{{
            folder.name
          }}</span>
        </div>
        <FolderTree
          v-if="folder.children.length > 0 && openFolders[folder.id]"
          :folders="folder.children"
          :selectedFolderId="selectedFolderId"
          @select="onSelect"
        />
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, PropType } from "vue";

interface Folder {
  id: number;
  name: string;
  children: Folder[];
}

export default defineComponent({
  name: "FolderTree",
  props: {
    folders: {
      type: Array as PropType<Folder[]>,
      required: true,
    },
    selectedFolderId: Number,
  },
  setup(props, { emit }) {
    const openFolders = ref<{ [key: number]: boolean }>({});

    const onSelect = (folderId: number) => {
      openFolders.value[folderId] = !openFolders.value[folderId];
      if (openFolders.value[folderId]) {
        emit("select", folderId);
      } else {
        emit("select", null);
      }
    };

    return {
      openFolders,
      onSelect,
    };
  },
});
</script>

<style scoped>
.selected {
  font-weight: bold;
}
</style>
