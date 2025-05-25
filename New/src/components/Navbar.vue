<template>
  <div class="sidebar">
    <div class="sidebar-header">
      <img src="" alt="Logo" class="logo" />
      <h1>Code and Cloud Academy</h1>
    </div>

    <ul class="menu">
      <li>
        <i class="icon">🏠</i>
        <span>Home</span>
      </li>
      <li>
        <i class="icon">📢</i>
        <span>Announcements</span>
      </li>
      <li @click="toggleAccordion" class="accordion-toggle">
        <i class="icon">📦</i>
        <span>Modules</span>
        <span class="chevron">{{ isOpen ? '▲' : '▼' }}</span>
      </li>
      <ul v-show="isOpen" class="submenu">
        <li>Module 1</li>
        <li>Module 2</li>
        <li>Module 3</li>
      </ul>
      <li>
        <i class="icon">📝</i>
        <span>Assignments</span>
      </li>
      <li>
        <i class="icon">📅</i>
        <span>Attendance</span>
      </li>
      <li>
        <i class="icon">📊</i>
        <span>Grades</span>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const isOpen = ref(false)

function toggleAccordion() {
  isOpen.value = !isOpen.value
}
</script>

<style scoped>
.sidebar {
  width: 240px;
  height: 100vh;
  background-color: #2e2e2e;
  color: #fff;
  padding: 20px;
  box-sizing: border-box;
}

.sidebar-header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 30px;
}

.logo {
  width: 32px;
  height: 32px;
}

.sidebar-header h1 {
  font-size: 16px;
  font-weight: bold;
}

.menu {
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px 10px;
  cursor: pointer;
  transition: background 0.3s;
}

.menu li:hover {
  background-color: #3f3f3f;
}

.icon {
  font-size: 18px;
}

.accordion-toggle {
  justify-content: space-between;
}

.submenu {
  list-style: none;
  padding-left: 24px;
  margin: 0;
}

.submenu li {
  padding: 6px 0;
  color: #ccc;
}
</style>