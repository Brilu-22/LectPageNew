<!-- src/views/Assignments/Overview.vue -->
<template>
  <div class="assignments-overview">
    <h1>Assignments Overview</h1>
    
    <div class="actions">
      <router-link to="/assignments/create" class="create-btn">
        Create New Assignment
      </router-link>
    </div>
    
    <div class="assignments-list">
      <div class="section">
        <h2>Upcoming Assignments</h2>
        
        <div class="assignment-card" v-for="assignment in upcomingAssignments" :key="assignment.id">
          <h3>{{ assignment.title }}</h3>
          <p>{{ assignment.description }}</p>
          <div class="meta">
            <span class="due-date">Due: {{ formatDate(assignment.dueDate) }}</span>
            <span class="format">Format: {{ assignment.submissionFormat }}</span>
          </div>
        </div>
      </div>
      
      <div class="section">
        <h2>Past Assignments</h2>
        
        <div class="assignment-card" v-for="assignment in pastAssignments" :key="assignment.id">
          <h3>{{ assignment.title }}</h3>
          <p>{{ assignment.description }}</p>
          <div class="meta">
            <span class="due-date">Due: {{ formatDate(assignment.dueDate) }}</span>
            <span class="format">Format: {{ assignment.submissionFormat }}</span>
          </div>
        </div>
      </div>
      
      <div class="section">
        <h2>Unpublished Assignments</h2>
        
        <div class="assignment-card" v-for="assignment in unpublishedAssignments" :key="assignment.id">
          <h3>{{ assignment.title }}</h3>
          <p>{{ assignment.description }}</p>
          <div class="meta">
            <span class="status">Draft</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// Sample data - in a real app, this would come from an API
const assignments = ref([
  {
    id: 1,
    title: 'API INTEGRATION: WEATHER DASHBOARD',
    description: 'Lorem ipsum dolor Sit Amet, Consectetur Adipiscing Elit..',
    dueDate: new Date('2023-06-15'),
    submissionFormat: 'code',
    status: 'published'
  },
  {
    id: 2,
    title: 'REFACTOR LEGACY CODE: E-COMMERCE CHECKOUT SYSTEM',
    description: 'Lorem ipsum dolor Sit Amet, Consectetur Adipiscing Elit..',
    dueDate: new Date('2023-06-20'),
    submissionFormat: 'zip',
    status: 'published'
  },
  {
    id: 3,
    title: 'DEBUGGING CHALLENGE: BANKING SYSTEM VULNERABILITY',
    description: 'Lorem ipsum dolor Sit Amet, Consectetur Adipiscing Elit..',
    dueDate: new Date('2023-05-10'),
    submissionFormat: 'pdf',
    status: 'published'
  },
  {
    id: 4,
    title: 'ALGORITHM CHALLENGE: ROUTE OPTIMISER FOR DELIVERY DRONES',
    description: 'Lorem ipsum dolor Sit Amet, Consectetur Adipiscing Elit..',
    dueDate: new Date('2023-05-05'),
    submissionFormat: 'code',
    status: 'published'
  },
  {
    id: 5,
    title: 'DEBUGGING CHALLENGE: BANKING SYSTEM VULNERABILITY',
    description: 'Lorem ipsum dolor Sit Amet, Consectetur Adipiscing Elit..',
    dueDate: null,
    submissionFormat: '',
    status: 'draft'
  },
  {
    id: 6,
    title: 'ALGORITHM CHALLENGE: ROUTE OPTIMISER FOR DELIVERY DRONES',
    description: 'Lorem ipsum dolor Sit Amet, Consectetur Adipiscing Elit..',
    dueDate: null,
    submissionFormat: '',
    status: 'draft'
  }
])

const upcomingAssignments = computed(() => {
  const today = new Date()
  return assignments.value.filter(a => 
    a.status === 'published' && 
    a.dueDate && 
    new Date(a.dueDate) >= today
  )
})

const pastAssignments = computed(() => {
  const today = new Date()
  return assignments.value.filter(a => 
    a.status === 'published' && 
    a.dueDate && 
    new Date(a.dueDate) < today
  )
})

const unpublishedAssignments = computed(() => {
  return assignments.value.filter(a => a.status === 'draft')
})

const formatDate = (date) => {
  if (!date) return 'Not set'
  return new Date(date).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  })
}
</script>

<style scoped>
.assignments-overview {
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  font-size: 24px;
  margin-bottom: 30px;
}

.actions {
  margin-bottom: 30px;
}

.create-btn {
  display: inline-block;
  background-color: #4CAF50;
  color: white;
  padding: 10px 15px;
  border-radius: 4px;
  text-decoration: none;
  font-weight: 500;
  transition: background-color 0.3s;
}

.create-btn:hover {
  background-color: #45a049;
}

.section {
  margin-bottom: 40px;
}

.section h2 {
  font-size: 18px;
  margin-bottom: 15px;
  padding-bottom: 8px;
  border-bottom: 1px solid #eee;
}

.assignment-card {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: var(--shadow-sm);
  margin-bottom: 15px;
}

.assignment-card h3 {
  margin-top: 0;
  margin-bottom: 10px;
  font-size: 16px;
}

.assignment-card p {
  margin-top: 0;
  margin-bottom: 15px;
  color: #555;
}

.meta {
  font-size: 14px;
  color: #777;
}

.meta span {
  display: inline-block;
  margin-right: 15px;
}

.status {
  color: #ff9800;
  font-weight: 500;
}
</style>