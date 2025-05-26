<template>
  <div class="app-container">
    <!-- Fixed Sidebar -->
    <div class="sidebar">
      <div class="sidebar-header">
        <i data-lucide="school" class="logo-icon"></i>
        <h1>Code and Cloud Academy</h1>
      </div>

      <ul class="menu">
        <li :class="{ active: activeMenu === 'home' }" @click="activeMenu = 'home'">
          <i data-lucide="home" class="icon"></i>
          <span>Home</span>
        </li>
        <li :class="{ active: activeMenu === 'announcements' }" @click="activeMenu = 'announcements'">
          <i data-lucide="megaphone" class="icon"></i>
          <span>Announcements</span>
        </li>
        <li @click="toggleAccordion" class="accordion-toggle">
          <i data-lucide="book-open" class="icon"></i>
          <span>Modules</span>
          <i data-lucide="chevron-down" class="chevron" :class="{ rotated: isOpen }"></i>
        </li>
        <ul v-show="isOpen" class="submenu">
          <li v-for="module in modules" :key="module.id">{{ module.name }}</li>
        </ul>
        <li :class="{ active: activeMenu === 'assignments' }" @click="activeMenu = 'assignments'">
          <i data-lucide="clipboard-list" class="icon"></i>
          <span>Assignments</span>
        </li>
        <li :class="{ active: activeMenu === 'attendance' }" @click="activeMenu = 'attendance'">
          <i data-lucide="calendar-check" class="icon"></i>
          <span>Attendance</span>
        </li>
        <li :class="{ active: activeMenu === 'grades' }" @click="activeMenu = 'grades'">
          <i data-lucide="bar-chart-2" class="icon"></i>
          <span>Grades</span>
        </li>
      </ul>
    </div>

    <!-- Main Content -->
    <div class="main-content">
      <div class="content-container">
        <header class="page-header">
          <h2>Create An Announcement</h2>
          <div class="underline"></div>
        </header>

        <section class="form-section">
          <h3>Create announcement</h3>
          <div class="form-underline"></div>

          <form @submit.prevent="handleSubmit">
            <div class="form-group">
              <label for="title">Announcement Title</label>
              <input
                id="title"
                v-model="title"
                type="text"
                placeholder="Type announcement title here"
                class="input"
                required
              />
            </div>

            <div class="form-group">
              <label for="body">Announcement Body</label>
              <div class="document-editor">
                <div class="toolbar">
                  <button type="button" @click="formatText('bold')" title="Bold">
                    <i data-lucide="bold"></i>
                  </button>
                  <button type="button" @click="formatText('italic')" title="Italic">
                    <i data-lucide="italic"></i>
                  </button>
                  <button type="button" @click="formatText('underline')" title="Underline">
                    <i data-lucide="underline"></i>
                  </button>
                  <select v-model="headingLevel" @change="formatHeading" class="heading-select">
                    <option value="">Normal Text</option>
                    <option value="h1">Heading 1</option>
                    <option value="h2">Heading 2</option>
                    <option value="h3">Heading 3</option>
                  </select>
                  <button type="button" @click="insertBulletList" title="Bullet List">
                    <i data-lucide="list"></i>
                  </button>
                  <button type="button" @click="insertNumberedList" title="Numbered List">
                    <i data-lucide="list-ordered"></i>
                  </button>
                </div>
                <div 
                  id="body"
                  class="document-content"
                  contenteditable="true"
                  placeholder="Type announcement body here"
                  @input="updateContent"
                ></div>
              </div>
            </div>

            <button type="submit" class="submit-button">
              <i data-lucide="send"></i>
              Send Announcement
            </button>
          </form>
        </section>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const isOpen = ref(false);
const headingLevel = ref('');
const content = ref('');
const title = ref('');
const activeMenu = ref('announcements');

const modules = ref([
  { id: 1, name: 'Module 1: Introduction' },
  { id: 2, name: 'Module 2: Core Concepts' },
  { id: 3, name: 'Module 3: Advanced Topics' }
]);

const toggleAccordion = () => {
  isOpen.value = !isOpen.value;
  // Update chevron icon
  nextTick(() => lucide.createIcons());
};

const formatText = (format) => {
  document.execCommand(format, false, null);
  document.getElementById('body').focus();
};

const formatHeading = () => {
  if (headingLevel.value) {
    document.execCommand('formatBlock', false, headingLevel.value);
  } else {
    document.execCommand('formatBlock', false, '<p>');
  }
  document.getElementById('body').focus();
};

const insertBulletList = () => {
  document.execCommand('insertUnorderedList', false, null);
  document.getElementById('body').focus();
};

const insertNumberedList = () => {
  document.execCommand('insertOrderedList', false, null);
  document.getElementById('body').focus();
};

const updateContent = (event) => {
  content.value = event.target.innerHTML;
};

const handleSubmit = () => {
  console.log('Announcement submitted:', {
    title: title.value,
    content: content.value
  });
  // Reset form
  title.value = '';
  content.value = '';
  document.getElementById('body').innerHTML = '';
};
</script>

<style>
/* Base Styles */
:root {
  --sidebar-bg: #D0DFCC;
  --sidebar-text: #212121;
  --primary: #4a6b57;
  --primary-hover: #3a5a47;
  --border-radius: 8px;
  --shadow: 0 2px 10px rgba(0,0,0,0.05);
}

html, body {
  margin: 0;
  padding: 0;
  min-height: 100%;
  height: auto;
  width: 100%;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
}

.app-container {
  display: flex;
  background-color: #f7f6fb;
  color: #212121;
  min-height: 100vh;
}

/* Sidebar Styles */
.sidebar {
  width: 280px;
  height: 100vh;
  position: fixed;
  background-color: var(--sidebar-bg);
  color: var(--sidebar-text);
  padding: 30px;
  box-sizing: border-box;
  z-index: 100;
  overflow-y: auto;
  border-right: 1px solid rgba(0,0,0,0.1);
}

.sidebar-header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 30px;
}

.logo-icon {
  width: 32px;
  height: 32px;
  color: var(--primary);
}

.sidebar-header h1 {
  font-size: 16px;
  font-weight: 600;
  color: var(--sidebar-text);
  margin: 0;
}

.menu {
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu li {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 10px;
  cursor: pointer;
  transition: all 0.2s;
  border-radius: var(--border-radius);
  margin-bottom: 4px;
}

.menu li:hover {
  background-color: rgba(0, 0, 0, 0.05);
}

.menu li.active {
  background-color: var(--primary);
  color: white;
}

.menu li.active .icon {
  color: white;
}

.icon {
  width: 18px;
  height: 18px;
}

.accordion-toggle {
  justify-content: space-between;
}

.chevron {
  transition: transform 0.2s;
}

.chevron.rotated {
  transform: rotate(180deg);
}

.submenu {
  list-style: none;
  padding-left: 34px;
  margin: 8px 0;
}

.submenu li {
  padding: 8px 0;
  color: #555;
  font-size: 14px;
}

/* Main Content Styles */
.main-content {
  margin-left: 280px;
  flex: 1;
  padding: 2rem;
  background-color: #fff;
  min-height: 100vh;
}

.content-container {
  max-width: 800px;
  margin: 0 auto;
  width: 100%;
}

.page-header {
  margin-bottom: 2rem;
}

.page-header h2 {
  font-size: 1.75rem;
  margin-bottom: 0.75rem;
  color: var(--primary);
  font-weight: 600;
}

.underline {
  width: 100%;
  height: 1px;
  background-color: #e2e8f0;
  margin-bottom: 2rem;
}

.form-section {
  padding: 2rem;
  background: #fff;
  border-radius: var(--border-radius);
  box-shadow: var(--shadow);
}

.form-section h3 {
  font-size: 1.25rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
  color: #4a5568;
}

.form-underline {
  width: min(100%, 240px);
  height: 1px;
  background-color: #cbd5e0;
  margin-bottom: 1.5rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
  color: #4a5568;
}

.input {
  width: 100%;
  padding: 0.75rem 1rem;
  border-radius: var(--border-radius);
  border: 1px solid #e2e8f0;
  background-color: #f8fafc;
  font-size: 1rem;
  transition: border-color 0.2s;
}

.input:focus {
  outline: none;
  border-color: var(--primary);
}

/* Document Editor Styles */
.document-editor {
  width: 100%;
  border-radius: var(--border-radius);
  border: 1px solid #e2e8f0;
  background-color: #f8fafc;
  overflow: hidden;
  min-height: 200px;
}

.toolbar {
  padding: 0.5rem;
  background-color: #edf2f7;
  border-bottom: 1px solid #e2e8f0;
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.toolbar button {
  padding: 0.5rem;
  border: 1px solid #e2e8f0;
  border-radius: 4px;
  background-color: white;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s;
}

.toolbar button:hover {
  background-color: #ebf8ff;
  border-color: #bee3f8;
}

.heading-select {
  padding: 0.5rem;
  border: 1px solid #e2e8f0;
  border-radius: 4px;
  background-color: white;
  cursor: pointer;
}

.document-content {
  padding: 1rem;
  outline: none;
  line-height: 1.6;
  min-height: 150px;
  overflow-y: auto;
}

.document-content:empty:before {
  content: attr(placeholder);
  color: #a0aec0;
  pointer-events: none;
  display: block;
}

/* Button Styles */
.submit-button {
  background-color: var(--primary);
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  border-radius: var(--border-radius);
  cursor: pointer;
  transition: background-color 0.3s;
  margin-top: 1.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  width: 100%;
  max-width: 200px;
  margin-left: auto;
  margin-right: auto;
  font-weight: 500;
}

.submit-button:hover {
  background-color: var(--primary-hover);
}

/* Responsive Adjustments */
@media (max-width: 992px) {
  .sidebar {
    width: 240px;
    padding: 20px;
  }
  
  .main-content {
    margin-left: 240px;
    padding: 1.5rem;
  }
}

@media (max-width: 768px) {
  .sidebar {
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    width: 260px;
  }
  
  .sidebar.active {
    transform: translateX(0);
  }
  
  .main-content {
    margin-left: 0;
    padding: 1rem;
  }
  
  .menu-toggle {
    display: block;
    position: fixed;
    top: 1rem;
    left: 1rem;
    z-index: 1000;
  }
}

@media (max-width: 480px) {
  .form-section {
    padding: 1.5rem;
  }
  
  .submit-button {
    max-width: 100%;
  }
  
  .toolbar {
    gap: 0.25rem;
  }
}
</style>