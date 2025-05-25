<!-- src/App.vue -->
<template>
  <Create />
</template>

<script setup>
import Create from '@/views/Announcement/Create.vue'
</script>

<style>
:root {
  --primary-color: #D0DFCC;
  --secondary-color: #ffffff;
  --text-color: #212121;
  --border-radius: 21px;
  --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  color: var(--text-color);
  background-color: #f7f6fb;
}
</style>