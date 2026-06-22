<script setup>
import { ref, computed, watch } from "vue"

import Header from "./components/Header.vue"
import Stats from "./components/Stats.vue"
import StudentForm from "./components/StudentForm.vue"
import StudentList from "./components/StudentList.vue"

const etudiants = ref(
  JSON.parse(
    localStorage.getItem(
      "students"
    )
  ) || []
)
const recherche = ref("")
const filiereSelectionnee = ref("Toutes")

// Sauvegarder les étudiants dans le localStorage à chaque modification
watch(etudiants, () => {
  localStorage.setItem("students", JSON.stringify(etudiants.value))
}, { deep: true })

function ajouterEtudiant(etudiant){

  etudiants.value.push({
    id: Date.now(),
    ...etudiant
  })

}

const etudiantsFiltres = computed(() => {

  let resultat = etudiants.value

  if(
    filiereSelectionnee.value !== "Toutes"
  ){
    resultat = resultat.filter(
      e =>
        e.filiere ===
        filiereSelectionnee.value
    )
  }

  return resultat.filter(
    e =>
      `${e.nom} ${e.prenom}`
      .toLowerCase()
      .includes(
        recherche.value.toLowerCase()
      )
  )

})

const total = computed(
  () => etudiantsFiltres.value.length
)

function supprimerEtudiant(id){

  if(
    !confirm(
      "Supprimer cet étudiant ?"
    )
  ){
    return
  }

  etudiants.value =
    etudiants.value.filter(
      e => e.id !== id
    )

}

function modifierEtudiant(id){

  const etudiant =
    etudiants.value.find(
      e => e.id === id
    )

  if(!etudiant) return

  const nouveauNom =
    prompt(
      "Modifier le nom",
      etudiant.nom
    )

  if(
    nouveauNom &&
    nouveauNom.trim() !== ""
  ){
    etudiant.nom = nouveauNom
  }

}
</script>

<template>

  <div class="container">

    <Header />

    <Stats
      :total="total"
    />

    <div class="search-box">

      <input
        v-model="recherche"
        placeholder="Rechercher un étudiant..."
      />

    </div>

    <div class="filters">

      <button
        @click="
          filiereSelectionnee='Toutes'
        "
      >
        Toutes
      </button>

      <button
        @click="
          filiereSelectionnee='Informatique'
        "
      >
        Informatique
      </button>

      <button
        @click="
          filiereSelectionnee='Réseaux'
        "
      >
        Réseaux
      </button>

      <button
        @click="
          filiereSelectionnee='Télécom'
        "
      >
        Télécom
      </button>

    </div>

    <StudentForm
      @addStudent="ajouterEtudiant"
    />

    <StudentList
      :students="etudiantsFiltres"
      @deleteStudent="supprimerEtudiant"
      @editStudent="modifierEtudiant"
    />
  </div>
</template>


