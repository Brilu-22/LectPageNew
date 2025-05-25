<template>
  <div class="layout">
    <Sidebar />

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
          <textarea
            id="body"
            placeholder="Type announcement body here"
            class="textarea"
          />
        </div>

        <button class="submit-button">Send Announcement</button>
      </section>
    </div>
  </div>
</template>

<script setup>
import Sidebar from './components/Navbar.vue'
</script>

<style scoped>
.layout {
  display: flex;
  height: 100vh;
}

.content {
  flex: 1;
  padding: 40px;
  background-color: #f7f6fb;
  color: #212121;
}

.page-header h2 {
  font-size: 28px;
  margin-bottom: 6px;
}

.underline {
  width: 100%;
  height: 1px;
  background-color: #ccc;
  margin-bottom: 30px;
}

.form-section h3 {
  font-size: 18px;
  font-weight: normal;
  margin-bottom: 4px;
}

.form-underline {
  width: 240px;
  height: 1px;
  background-color: #aaa;
  margin-bottom: 24px;
}

.form-group {
  margin-bottom: 24px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
}

.input {
  width: 100%;
  padding: 12px 16px;
  border-radius: 20px;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
  font-size: 14px;
}

.textarea {
  width: 100%;
  height: 180px;
  padding: 16px;
  border-radius: 20px;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
  font-size: 14px;
  resize: vertical;
}

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
</style>