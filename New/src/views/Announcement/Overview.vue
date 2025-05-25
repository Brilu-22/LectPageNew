<template>
  <div class="p-6">
    <h1 class="text-2xl font-medium mb-4">Announcements Overview</h1>

    <!-- Filters -->
    <div class="flex items-center gap-4 mb-6">
      <input
        v-model="search"
        type="text"
        placeholder="Search"
        class="bg-gray-100 px-4 py-2 rounded-full w-1/3"
      />
      <select class="bg-gray-100 px-3 py-2 rounded" v-model="filter">
        <option value="all">All</option>
        <option value="important">Important</option>
      </select>
      <select class="bg-gray-100 px-3 py-2 rounded" v-model="dateSort">
        <option value="desc">Newest First</option>
        <option value="asc">Oldest First</option>
      </select>
      <RouterLink
        to="/announcements/create"
        class="ml-auto bg-gray-200 px-4 py-2 rounded-full text-sm font-medium"
      >
        Create New Announcement ✏️
      </RouterLink>
    </div>

    <!-- Announcements List -->
    <div v-for="announcement in filteredAnnouncements" :key="announcement.id"
         class="bg-gray-100 rounded-lg px-6 py-4 mb-3">
      <h3 class="font-semibold text-sm uppercase">
        {{ announcement.title }}
      </h3>
      <p class="text-sm text-gray-600 truncate">{{ announcement.body }}</p>
      <p class="text-xs text-right mt-2">
        Posted On: {{ formatDate(announcement.date) }}
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const search = ref('')
const filter = ref('all')
const dateSort = ref('desc')

const announcements = ref([
  {
    id: 1,
    title: 'Computer Science Workshop with Jacob Anderson',
    body: 'Lorem Ipsum Dolor Sit Amet, Consectetur Adipisicing Elit...',
    date: '2025-04-02T11:36:00'
  },
  // Add more demo data
])

const filteredAnnouncements = computed(() => {
  let results = announcements.value

  if (search.value) {
    results = results.filter(a => a.title.toLowerCase().includes(search.value.toLowerCase()))
  }

  if (dateSort.value === 'asc') {
    results = results.sort((a, b) => new Date(a.date).getTime() - new Date(b.date).getTime())
  } else {
    results = results.sort((a, b) => new Date(b.date).getTime() - new Date(a.date).getTime())
  }

  return results
})

const formatDate = (dateStr: string) => {
  const date = new Date(dateStr)
  return date.toLocaleString('en-GB', { dateStyle: 'medium', timeStyle: 'short' })
}
</script>