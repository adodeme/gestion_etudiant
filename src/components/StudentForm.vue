<script setup>
import { ref } from "vue"

const emit = defineEmits(["addStudent"])

const nom = ref("")
const prenom = ref("")
const filiere = ref("Informatique")
const photo = ref("")

function ajouter(){

  if(
    !nom.value.trim() ||
    !prenom.value.trim()
  ){
    return
  }

  emit("addStudent",{
    nom: nom.value,
    prenom: prenom.value,
    filiere: filiere.value,
    photo: photo.value,
  })

  nom.value=""
  prenom.value=""
}
</script>

<template>

  <div class="form">

    <input
      v-model="nom"
      placeholder="Nom"
    >

    <input
      v-model="prenom"
      placeholder="Prénom"
    >

    <select v-model="filiere">
      <option>Informatique</option>
      <option>Réseaux</option>
      <option>Télécom</option>
      <option>Gestion</option>
    </select>

    <input
    v-model="photo"
    placeholder="URL de la photo"
    />

    <div v-if="photo" class="preview">
        <img
            :src="photo"
            alt="Prévisualisation"
        />
    </div>

    <button @click="ajouter">
      Ajouter
    </button>

  </div>

</template>

<style scoped>
.form{
  display:grid;
  grid-template-columns:1fr 1fr 1fr 180px;
  gap:15px;
  align-items:center;
  margin-bottom:25px;
}

input,
select{
  padding:15px;
  border:none;
  border-radius:14px;
  background:white;
  box-shadow:0 10px 25px rgba(0,0,0,.05);
}

button{
  border:none;
  background:#111827;
  color:white;
  border-radius:14px;
  padding:15px 25px;
  font-size:16px;
  font-weight:600;
  min-height:55px;
  cursor:pointer;
  transition:0.3s;
}

button:hover{
  transform:translateY(-2px);
  background:#1e293b;
}

@media(max-width:768px){
  .form{
    grid-template-columns:1fr;
  }
}

.preview{
  margin-top:10px;
}

.preview img{
  width:100px;
  height:100px;
  border-radius:50%;
  object-fit:cover;
}
</style>