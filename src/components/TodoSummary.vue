<template>
  <div class="summary">
    <v-progress-circular :model-value="completionRate" :rotate="-90" :size="60" :width="6" :value="completionRate" color="orange-lighten-2" >
      {{ completionRate }}%
    </v-progress-circular>
    <span>남은 할 일: {{ remaining }}개</span>| <span>완료한 할 일: {{ completed }}개</span>
    <div class="progress">
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { toRefs } from 'vue'

const props = defineProps({
  todoList: {
    type: Array,
    required: true,
  },
})

const { todoList } = toRefs(props)

const remaining = computed(() => {
  return todoList.value.filter(todo => !todo.completed).length
})

const completed = computed(() => {
  return todoList.value.filter(todo => todo.completed).length
})

const completionRate = computed(() => {
  const total = todoList.value.length
  const completedCount = completed.value
  return total === 0 ? 0 : Math.round((completedCount / total) * 100)
})
</script>

<style scoped>
span{
  color: rgb(240, 176, 0);
}
.summary {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin-bottom : 10px;
  gap: 10px;

}
.progress {
  margin-left: auto;
}
</style>