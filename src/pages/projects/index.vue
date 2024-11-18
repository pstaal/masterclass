<script setup lang="ts">
import { projectsQuery } from '@/utils/supaQueries'
import { columns } from '@/utils/tableColumns/projectsColumns'
import type { Projects } from '@/utils/supaQueries'
import {useProjectsStore} from "@/stores/loaders/projects";
import {storeToRefs} from "pinia";
import {useCollabs} from "@/composables/collabs";

usePageStore().pageData.title = 'Projects'

const projectsLoader = useProjectsStore()
const { projects } = storeToRefs(projectsLoader)
const { getProjects } = projectsLoader
await getProjects()

const { getGroupedCollabs, groupedCollabs } = useCollabs()

getGroupedCollabs(projects.value )

const columnsWithCollabs = columns(groupedCollabs)
</script>

<template>
  <DataTable v-if="projects" :columns="columnsWithCollabs" :data="projects" />
</template>
