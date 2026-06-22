<script setup>
import StudentItem from "./StudentItem.vue"

defineProps({
  students:Array
})

const emit = defineEmits([
  "deleteStudent",
  "editStudent"
])
</script>

<template>

  <div class="list">

    <StudentItem
        v-for="student in students"
        :key="student.id"
        :student="student"
        @deleteStudent="emit('deleteStudent',$event)"
        @editStudent="emit('editStudent',$event)"
    />

  </div>

</template>

<style scoped>
.list{
  display:flex;
  flex-direction:column;
  gap:15px;
}
</style>