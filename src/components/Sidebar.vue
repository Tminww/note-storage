<template>
  <div class="w-1/4 bg-gray-100 p-4">
    <button @click="createFolder" class="mb-4">+ Новая папка</button>
    <ul>
      <li v-for="folder in folders" :key="folder" @click="$emit('folder-selected', folder)">
        {{ folder }}
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { readDir, createDir } from '@tauri-apps/api/fs';

const folders = ref([]);

onMounted(loadFolders);

async function loadFolders() {
  folders.value = (await readDir('notes', { recursive: false })).map(f => f.name);
}

async function createFolder() {
  const name = prompt('Имя папки:');
  if (name) {
    await createDir(`notes/${name}`);
    loadFolders();
  }
}
</script>