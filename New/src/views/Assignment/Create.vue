<!-- src/views/Assignments/Create.vue -->
<template>
  <div class="assignments-create">
    <h1>Assignments Overview</h1>
    
    <div class="form-container">
      <h2>Create a New Assignment</h2>
      
      <div class="form-group">
        <label>Assignment Title</label>
        <input 
          type="text" 
          v-model="assignment.title"
          placeholder="Type assignment title here"
          class="form-input"
        >
      </div>
      
      <div class="form-group">
        <label>Assignment Due Date</label>
        <input 
          type="date" 
          v-model="assignment.dueDate"
          class="form-input"
        >
      </div>
      
      <div class="form-group">
        <label>Expected Submission Format</label>
        <select v-model="assignment.submissionFormat" class="form-input">
          <option value="">Select a Format</option>
          <option value="pdf">PDF</option>
          <option value="doc">Word Document</option>
          <option value="zip">ZIP Archive</option>
          <option value="code">Source Code</option>
        </select>
      </div>
      
      <div class="form-group">
        <label>Assignment Details Header</label>
        <input 
          type="text" 
          v-model="assignment.detailsHeader"
          placeholder="Type assignment title here"
          class="form-input"
        >
      </div>
      
      <div class="form-group">
        <label>Assignment Details Description</label>
        <textarea 
          v-model="assignment.detailsDescription"
          placeholder="Type assignment Description Here"
          class="form-textarea"
          rows="6"
        ></textarea>
      </div>
      
      <button @click="saveAssignment" class="submit-btn">
        SAVE ASSIGNMENT
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const assignment = ref({
  title: '',
  dueDate: '',
  submissionFormat: '',
  detailsHeader: '',
  detailsDescription: ''
})

const saveAssignment = () => {
  // In a real app, you would send this to your backend
  console.log('Assignment saved:', assignment.value)
  router.push('/assignments')
}
</script>

<style scoped>
.assignments-create {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  font-size: 24px;
  margin-bottom: 30px;
}

h2 {
  font-size: 20px;
  margin-bottom: 20px;
}

.form-container {
  background: white;
  padding: 30px;
  border-radius: 8px;
  box-shadow: var(--shadow-sm);
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
}

.form-input, .form-textarea, select {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-family: inherit;
}

.form-textarea {
  min-height: 150px;
  resize: vertical;
}

.submit-btn {
  background-color: #4CAF50;
  color: white;
  border: none;
  padding: 12px 20px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.3s;
}

.submit-btn:hover {
  background-color: #45a049;
}
</style>