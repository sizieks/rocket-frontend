<template>
  <leads-table
    :data-source="dataSource"
    :loading="loading"
    @search="handleSearch"
  />
</template>

<script setup lang="ts">
import { ref, onBeforeMount } from 'vue';
import { ILead } from './types';
import LeadsTable from './components/LeadsTable.vue';

const loading = ref(true);
const dataSource = ref<ILead[]>([]);
const currentQuery = ref('');
const URL = 'http://localhost:3000/leads';

const handleSearch = async (query: string) => {
  if (currentQuery.value !== query) {
    currentQuery.value = query;
    loading.value = true;
    dataSource.value = await fetch(`${URL}?user=${query}`).then((response) =>
      response.json()
    );
    loading.value = false;
  }
};

onBeforeMount(async () => {
  dataSource.value = await fetch(URL).then((response) => response.json());
  loading.value = false;
});
</script>

<style scoped></style>
./types
