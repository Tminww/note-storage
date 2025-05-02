<template>
  <div class="flex-1 p-4">
    <textarea v-model="content" class="w-full h-full resize-none"></textarea>
    <button @click="saveNote" class="mt-2">Сохранить</button>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { readTextFile, writeFile } from '@tauri-apps/plugin-fs';

const props = defineProps({ notePath: String });
const content = ref('');

watch(() => props.notePath, async (path) => {
  if (path) {
    content.value = await readTextFile(`notes/${path}`);
  }
});

async function saveNote() {
  if (props.notePath) {
    await writeFile({ path: `notes/${props.notePath}`, contents: content.value });
    alert('Сохранено');
  }
}
</script>
