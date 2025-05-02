<template>
  <div class="flex h-screen">
    hui
    <Sidebar @folder-selected="selectFolder" />
    <NotesList :folder="selectedFolder" @note-selected="selectNote" />
    <NoteEditor :notePath="selectedNote" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { default as Sidebar} from './components/Sidebar.vue';
import { default as NotesList }from './components/NotesList.vue';
import { default as NoteEditor} from './components/NoteEditor.vue';

const selectedFolder = ref(null);
const selectedNote = ref(null);

function selectFolder(folder) {
  selectedFolder.value = folder;
  selectedNote.value = null;
}

function selectNote(note) {
  selectedNote.value = note;
}
</script>