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

    <!-- Main Content -->
    <div class="main-content">
      <div class="content-container">
        <header class="page-header">
          <h2>Create An Announcement</h2>
          <div class="underline" />
        </header>

        <section class="form-section">
          <h3>Create an Announcement</h3>
          <div class="form-underline" />

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
                  <button type="button" @click="formatText('bold')" title="Bold"><strong>B</strong></button>
                  <button type="button" @click="formatText('italic')" title="Italic"><em>I</em></button>
                  <button type="button" @click="formatText('underline')" title="Underline"><u>U</u></button>
                  <select v-model="headingLevel" @change="formatHeading">
                    <option value="">Normal Text</option>
                    <option value="h1">Heading 1</option>
                    <option value="h2">Heading 2</option>
                    <option value="h3">Heading 3</option>
                  </select>
                  <button type="button" @click="insertBulletList" title="Bullet List">• List</button>
                  <button type="button" @click="insertNumberedList" title="Numbered List">1. List</button>
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

            <button type="submit" class="submit-button">Send Announcement</button>
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

const toggleAccordion = () => {
  isOpen.value = !isOpen.value;
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
  // Add your submission logic here
};
</script>

<style scoped>
/* Base Styles */

html, body {
  margin: 0;
  padding: 0;
  min-height: 100%;
  height: auto;
  width: 100%;
}

.app-container {
  display: flex;
  background-color: #f7f6fb;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  color: #212121;
  flex-direction: row; /* keep this for sidebar + content layout */
  align-items: flex-start;
  min-height: 100%;
}

/* Sidebar Styles */
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
  border-radius: 4px;
}

.menu li:hover {
  background-color: rgba(0, 0, 0, 0.1);
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
  color: #555;
}

/* Main Content Styles */
.main-content {
  margin-left: 280px;
  flex: 1;
  padding: 2rem;
  background-color: #fff;
  min-height: 100%;
  height: auto;
  overflow-y: auto;
}

.content-container {
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

.page-header {
  margin-bottom: 2rem;
}

.page-header h2 {
  font-size: clamp(1.5rem, 2vw, 2rem);
  margin-bottom: 0.5rem;
}

.underline {
  width: 100%;
  height: 1px;
  background-color: #ccc;
  margin-bottom: 2rem;
}

.form-section {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}

.form-section h3 {
  font-size: clamp(1rem, 1.2vw, 1.25rem);
  font-weight: normal;
  margin-bottom: 0.25rem;
}

.form-underline {
  width: min(100%, 240px);
  height: 1px;
  background-color: #aaa;
  margin-bottom: 1.5rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.input {
  width: 100%;
  padding: 0.75rem 1rem;
  border-radius: 20px;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
  font-size: 1rem;
}

/* Document Editor Styles */
.document-editor {
  width: 100%;
  border-radius: 20px;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
  overflow: hidden;
  min-height: 200px;
}

.toolbar {
  padding: 0.5rem;
  background-color: #e9e9e9;
  border-bottom: 1px solid #ccc;
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.toolbar button {
  padding: 0.25rem 0.5rem;
  border: 1px solid #ccc;
  border-radius: 10px;
  background-color: #f1f1f1;
  cursor: pointer;
}

.toolbar select {
  padding: 0.25rem 0.5rem;
  border: 1px solid #ccc;
  border-radius: 10px;
  background-color: #f1f1f1;
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
  color: #999;
  pointer-events: none;
  display: block;
}

/* Button Styles */
.submit-button {
  background-color: #D0DFCC;
  color: #212121;
  border: none;
  padding: 12px 32px;
  font-size: 14px;
  border-radius: 20px;
  cursor: pointer;
  transition: background-color 0.3s;
  margin-top: 1rem;
  display: block;
  width: 100%;
  max-width: 200px;
  margin-left: auto;
  margin-right: auto;
}

.submit-button:hover {
  background-color: #c0cfbc;
}

/* Responsive Adjustments */
@media (max-width: 992px) {
  .sidebar {
    width: 200px;
    padding: 20px;
  }
  
  .main-content {
    margin-left: 200px;
    padding: 1.5rem;
  }
}

@media (max-width: 768px) {
  .sidebar {
    width: 60px;
    padding: 10px;
  }
  
  .sidebar-header h1, 
  .menu span {
    display: none;
  }
  
  .toolbar {
    gap: 0.25rem;
  }
  
  .toolbar select {
    width: 100%;
  }
  
  .document-editor {
    min-height: 150px;
  }
}

@media (max-width: 480px) {
  .sidebar {
    transform: translateX(-100%);
    transition: transform 0.3s ease;
  }
  
  .sidebar.active {
    transform: translateX(0);
  }
  
  .main-content {
    padding: 1rem;
    margin-left: 0;
  }
  
  .form-section {
    padding: 1rem;
  }
}
</style>