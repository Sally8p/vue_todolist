<template>
  <v-list-item :class="{ completed: todoItem.completed }">
    <v-list-item-content>
      <v-list-item-title @click.stop="toggleCompleted" :class="{ completed: todoItem.completed }">
        {{ todoItem.todo }}
      </v-list-item-title>
    </v-list-item-content>
    <v-list-item-action class="action-container">
      <span class="date">{{ formattedDate }}</span>
      <v-btn outlined color="teal-darken-1" @click.stop="$emit('delete-todo', todoItem.id)" class="delete-btn">
        삭제
        <v-icon>mdi-delete</v-icon>
      </v-btn>
    </v-list-item-action>
  </v-list-item>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  todoItem: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['toggle-completed'])

const toggleCompleted = () => {
  emit('toggle-completed', props.todoItem.id)
}

const formattedDate = computed(() => {
  const date = new Date(props.todoItem.date)
  return `${date.getFullYear()}. ${date.getMonth() + 1}. ${date.getDate()}.`
})
</script>

<style scoped>
.completed {
  font-size: 15px;
  background-color: rgb(255, 189, 56);
  border-radius: 25px;
  margin: 10px 0 10px 0; 
}

.completed .v-list-item-title {
  text-decoration: line-through;
}

.v-btn {
  color: yellow;
  border-radius: 20px;
  text-transform: none; 
  box-shadow: none; 
}

.v-btn .v-icon {
  margin-left: 8px;
}

.v-list-item-action {
  display: flex;
  align-items: center;
  gap: 8px;
}

.date {
  margin-right: 8px;
  color: gray;
}

.action-container {
  margin-left: auto; 
}
</style>