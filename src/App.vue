<script setup>
import { ref, computed } from 'vue'

const nom = ref('')
const prenom = ref('')
const classe = ref('')
const recherche = ref('')

const etudiants = ref([])

function ajouterEtudiant() {
  if (
    nom.value.trim() === '' ||
    prenom.value.trim() === '' ||
    classe.value.trim() === ''
  ) {
    alert('Veuillez remplir tous les champs')
    return
  }

  etudiants.value.push({
    id: Date.now(),
    nom: nom.value,
    prenom: prenom.value,
    classe: classe.value
  })

  nom.value = ''
  prenom.value = ''
  classe.value = ''
}

function supprimerEtudiant(id) {
  etudiants.value = etudiants.value.filter(
    etudiant => etudiant.id !== id
  )
}

const etudiantsFiltres = computed(() => {
  return etudiants.value.filter(etudiant =>
    `${etudiant.nom} ${etudiant.prenom} ${etudiant.classe}`
      .toLowerCase()
      .includes(recherche.value.toLowerCase())
  )
})
</script>

<template>
  <div class="container">
    <h1>Gestion des Étudiants</h1>

    <div class="formulaire">
      <input
        v-model="nom"
        type="text"
        placeholder="Nom"
      />

      <input
        v-model="prenom"
        type="text"
        placeholder="Prénom"
      />

      <input
        v-model="classe"
        type="text"
        placeholder="Classe"
      />

      <button @click="ajouterEtudiant">
        Ajouter
      </button>
    </div>

    <div class="recherche">
      <input
        v-model="recherche"
        type="text"
        placeholder="Rechercher un étudiant..."
      />
    </div>

    <div class="liste">
      <div
        v-for="etudiant in etudiantsFiltres"
        :key="etudiant.id"
        class="carte"
      >
        <div>
          <h3>
            {{ etudiant.nom }}
            {{ etudiant.prenom }}
          </h3>

          <p>{{ etudiant.classe }}</p>
        </div>

        <button
          class="supprimer"
          @click="supprimerEtudiant(etudiant.id)"
        >
          Supprimer
        </button>
      </div>

      <p
        v-if="etudiantsFiltres.length === 0"
        class="vide"
      >
        Aucun étudiant trouvé
      </p>
    </div>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
}

.container {
  max-width: 1000px;
  margin: 40px auto;
  padding: 20px;
}

h1 {
  text-align: center;
  margin-bottom: 30px;
}

.formulaire {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 15px;
  margin-bottom: 25px;
}

input {
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 8px;
}

button {
  cursor: pointer;
  padding: 12px;
  border: none;
  border-radius: 8px;
}

.formulaire button {
  background: #729414;
  color: white;
}

.recherche {
  margin-bottom: 25px;
}

.recherche input {
  width: 100%;
}

.liste {
  display: grid;
  gap: 15px;
}

.carte {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ddd;
  padding: 18px;
  border-radius: 10px;
}

.carte h3 {
  margin-bottom: 5px;
}

.supprimer {
  background: crimson;
  color: white;
}

.vide {
  text-align: center;
  padding: 20px;
}
</style>