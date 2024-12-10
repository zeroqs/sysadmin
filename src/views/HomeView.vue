<script setup lang="ts">
import InputText from 'primevue/inputtext'
import { computed, ref } from 'vue'
import { data, filterOptions } from '@/utils/constants'
import Card from 'primevue/card'
import Select from 'primevue/select'

const searchValue = ref('')
const selectedType = ref()

const problems = computed(() => {
  return data.filter((item) => {
    const matchesSearch = item.title.toLowerCase().includes(searchValue.value.toLowerCase())
    const matchesType = selectedType.value ? item.type === selectedType.value.value : true
    return matchesSearch && matchesType
  })
})
</script>

<template>
  <main class="main">
    <div class="search">
      <InputText class="search-input" placeholder="Search" v-model="searchValue" />
      <Select
        v-model="selectedType"
        :options="filterOptions"
        optionLabel="label"
        placeholder="Тип проблемы"
      />
    </div>

    <h1 v-if="problems.length" class="title-problems">Список проблем:</h1>
    <div v-if="problems.length" class="problems">
      <Card v-for="problem in problems" :key="problem.title">
        <template #title>{{ problem.title }}</template>
        <template #subtitle>{{ problem.type }}</template>

        <template #content>
          <span class="problem">Описание проблемы: </span>
          <span class="m-0">
            {{ problem.description }}
          </span>
        </template>

        <template #footer>
          <span class="solution">Решение: </span>
          <span class="m-0">
            {{ problem.solution }}
          </span>
        </template>
      </Card>
    </div>
    <div v-else>
      <h1 class="title-empty">Список пуст 🤷‍♂️</h1>
    </div>
  </main>
</template>

<style scoped>
.search {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 8px;

  margin-top: 40px;
}

.search-input {
  width: 100%;
}

.title-problems {
  margin-top: 40px;
}

.problems {
  display: flex;
  flex-direction: column;
  gap: 16px;
  margin-top: 10px;
}

.problem {
  color: rgb(212, 19, 19);
}

.solution {
  color: rgb(9, 110, 9);
}

.title-empty {
  text-align: center;
  margin-top: 50px;
}
</style>
