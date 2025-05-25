<template>
  <div class="app-container">
    <!-- Fixed Sidebar -->
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

    <!-- Main Content Area -->
    <div class="main-content">
      <slot /> <!-- 👈 Page content goes here -->
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const isOpen = ref(false)

const toggleAccordion = () => {
  isOpen.value = !isOpen.value
}
</script>

<style scoped>
/* Layout styles exactly as in your page */
.app-container {
  display: flex;
  min-height: 100vh;
  background-color: #f7f6fb;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  color: #212121;
  overflow: hidden;
}

.sidebar {
  width: 280px;
  height: 100vh;
  position: fixed;
  background-color: #D0DFCC;
  color: #212121;
  padding: 30px;
  box-sizing: border-box;
  z-index: 100;
  overflow-y: auto;
}

/* (Add your sidebar-header, logo, menu, etc styles here...) */

.main-content {
  margin-left: 280px;
  flex: 1;
  padding: 2rem;
  background-color: #fff;
  min-height: 100vh;
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
  color: #212121;
}

</style>