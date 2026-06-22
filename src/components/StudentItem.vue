<script setup>
const { student } = defineProps({
  student: Object
})

const emit = defineEmits([
  "deleteStudent",
  "editStudent"
])

function supprimer(){
  emit("deleteStudent", student.id)
}

function modifier(){
  emit("editStudent", student.id)
}
</script>

<template>

  <div class="student-card">

    <div class="infos">

      <h3>
        {{ student.nom }}
        {{ student.prenom }}
      </h3>

      <span class="filiere">
        {{ student.filiere }}
      </span>

    </div>

    <div class="actions">

      <button
        class="edit-btn"
        @click="modifier"
      >
        Modifier
      </button>

      <button
        class="delete-btn"
        @click="supprimer"
      >
        Supprimer
      </button>

    </div>

  </div>

</template>

<style scoped>
.student-card{
  background:white;
  padding:20px;
  border-radius:18px;
  display:flex;
  justify-content:space-between;
  align-items:center;
  box-shadow:0 10px 25px rgba(0,0,0,.05);
}

.infos h3{
  color:#0f172a;
}

.filiere{
  display:inline-block;
  margin-top:8px;
  background:#e0f2fe;
  color:#0369a1;
  padding:6px 12px;
  border-radius:999px;
  font-size:13px;
}

.actions{
  display:flex;
  gap:10px;
}

.edit-btn{
  border:none;
  background:#2563eb;
  color:white;
  padding:10px 15px;
  border-radius:10px;
}

.delete-btn{
  border:none;
  background:#ef4444;
  color:white;
  padding:10px 15px;
  border-radius:10px;
}

@media(max-width:768px){
  .student-card{
    flex-direction:column;
    gap:15px;
  }
}
</style>