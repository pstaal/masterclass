<script setup lang="ts">
import { supabase } from '@/lib/supabaseClient'
import type { Tables } from '../../../database/types'
import { ref } from 'vue'
const projects = ref<Tables<'projects'>[] | null>(null)
;(async () => {
  const { error, data } = await supabase.from('projects').select()
  if (error) console.log(error)
  projects.value = data
  console.log(projects.value)
})()
</script>

<template>
  <div>
    <h1>Projects</h1>
    <RouterLink to="/">Go to home</RouterLink>
    <ul>
      <li v-for="project in projects" :key="project.id">{{ project.name }}</li>
    </ul>
  </div>
</template>
