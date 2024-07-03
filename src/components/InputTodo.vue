<template>
  <v-row class="mb-3">
    <v-col>
      <v-text-field
        v-model="todo"
        label="할일을 여기에 입력해주세요~🙏🏻"
        @keyup.enter="addTodoHandler"
        append-icon="mdi-apple"
        @click:append="addTodoHandler"
        outlined
        dense
        color="success"
        class="black-text no-details custom-text-field"
      ></v-text-field>
    </v-col>
  </v-row>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-todo'])
const todo = ref('')
const addTodoHandler = () => {
  if (todo.value.length >= 3) {
    emit('add-todo', todo.value)
    todo.value = ''
  }
}
</script>

<style>
.black-text .v-input__control .v-input__slot input {
  color: #000 !important;
}

.no-details .v-input__details {
  display: none;
}

.custom-text-field .v-input__append-inner {
  display: flex;
  align-items: center;
  padding-right: 16px;
}

.mdi-apple {
  font-size: 24px; /* 아이콘 크기 조정 */
  color: black;
  padding: 8px;
  background: #fff;
  border-radius: 10px;
}

.custom-text-field .v-icon {
  font-size: 35px;
  background: #fff;
  padding: 12px; /* 아이콘 배경 사이즈 조정 */
  border-radius: 50%; /* 아이콘 배경 원형으로 */
}

.v-text-field .v-field--no-label input, .v-text-field .v-field--active input {
  color: #000;
}

.line-none {
  border-bottom: none;
}

.custom-text-field .v-icon {
  background-color: #ffffff;
}

.v-input__details > .v-icon, .v-input__prepend > .v-icon, .v-input__append > .v-icon {
  opacity: 1 !important; /* 아이콘 투명도를 1로 설정 */
}

.v-input__append {
  background: #fff;
  border-radius: 10px;
  padding: 10px;
  align-items: center;
}
</style>