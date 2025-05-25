<template>
  <div class="layout">
    <Navbar /> 

    <div class="content">
      <header class="page-header">
        <h2>Create An Announcement</h2>
        <div class="underline" />
      </header>

      <section class="form-section">
        <h3>Create an Announcement</h3>
        <div class="form-underline" />

        <div class="form-group">
          <label for="title">Announcement Title</label>
          <input
            id="title"
            type="text"
            placeholder="Type announcement title here"
            class="input"
          />
        </div>

        <div class="form-group">
          <label for="body">Announcement Body</label>
          <div class="document-editor">
            <div class="toolbar">
              <button @click="formatText('bold')" title="Bold"><strong>B</strong></button>
              <button @click="formatText('italic')" title="Italic"><em>I</em></button>
              <button @click="formatText('underline')" title="Underline"><u>U</u></button>
              <select v-model="headingLevel" @change="formatHeading">
                <option value="">Normal Text</option>
                <option value="h1">Heading 1</option>
                <option value="h2">Heading 2</option>
                <option value="h3">Heading 3</option>
              </select>
              <button @click="insertBulletList" title="Bullet List">• List</button>
              <button @click="insertNumberedList" title="Numbered List">1. List</button>
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

        <button class="submit-button">Send Announcement</button>
      </section>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Navbar from '@/components/Navbar.vue';

const headingLevel = ref('');
const content = ref('');

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
</script>

<style scoped>
/* All your original styling remains exactly the same */
.layout {
  margin-left: 300px;
  width: 100%;
  height: 100vh;
  display: flex;
}

.content {
  flex: 3;
  padding: 2rem;
  background-color: #f7f6fb;
  color: #212121;
  display: flex;
  flex-direction: column;
  overflow: auto;
}

.page-header h2 {
  margin-bottom: 0.5rem;
}

.underline {
  width: 100%;
  height: 1px;
  background-color: #ccc;
  margin-bottom: 2rem;
}

.form-section {
  flex: 1;
  display: flex;
  flex-direction: column;
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
  flex: 1;
  display: flex;
  flex-direction: column;
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

/* New document editor styles that match your original design */
.document-editor {
  width: 100%;
  border-radius: 20px;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
  overflow: hidden;
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
  min-height: 180px;
  padding: 1rem;
  outline: none;
  line-height: 1.6;
}

.document-content:empty:before {
  content: attr(placeholder);
  color: #999;
  pointer-events: none;
  display: block;
}

/* Your original button styling */
.submit-button {
  background-color: #d0dfcc;
  border: none;
  padding: 12px 32px;
  font-size: 14px;
  border-radius: 20px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.submit-button:hover {
  background-color: #c0cfbc;
}

@media (max-width: 768px) {
  .content {
    padding: 1rem;
  }
  
  .document-content {
    min-height: 150px;
  }
}
</style>