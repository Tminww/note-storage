<template>
  <div class="flex h-screen">
    <Sidebar @folder-selected="selectFolder" />
    <NotesList :folder="selectedFolder" @note-selected="selectNote" />
    <NoteEditor :notePath="selectedNote" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Sidebar from './components/Sidebar.vue';
import NotesList from './components/NotesList.vue';
import NoteEditor from './components/NoteEditor.vue';

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