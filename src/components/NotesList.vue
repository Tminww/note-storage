<template>
  <div class="w-1/4 bg-white p-4">
    <button @click="createNote" class="mb-4">+ Новая заметка</button>
    <ul>
      <li v-for="note in notes" :key="note" @click="$emit('note-selected', note)">
        {{ note }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { readTextFile, writeFile } from '@tauri-apps/plugin-fs';

const props = defineProps({ folder: String });
const notes = ref([]);

watch(() => props.folder, async (folder) => {
  if (folder) {
    notes.value = (await readDir(`notes/${folder}`)).map(f => f.name);
  }
});

async function createNote() {
  const name = prompt('Имя заметки:');
  if (name) {
    const path = `notes/${props.folder}/${name}.md`;
    await writeFile({ path, contents: '# Новая заметка' });
    notes.value.push(`${name}.md`);
  }
}
</script>