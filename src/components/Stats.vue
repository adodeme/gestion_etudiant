<script setup>
defineProps({
  total:Number,
  informatique:Number,
  reseaux:Number,
  telecom:Number,
  gestion:Number
})
</script>

<template>

  <div class="stats">

    <div class="card">
      <h2>{{ total }}</h2>
      <span>Total</span>
    </div>

    <div class="card">
      <h2>{{ informatique }}</h2>
      <span>Informatique</span>
    </div>

    <div class="card">
      <h2>{{ reseaux }}</h2>
      <span>Réseaux</span>
    </div>

    <div class="card">
      <h2>{{ telecom }}</h2>
      <span>Télécom</span>
    </div>

    <div class="card">
      <h2>{{ gestion }}</h2>
      <span>Gestion</span>
    </div>

  </div>

</template>

<style scoped>
.stats{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
  gap:20px;
  margin-bottom:30px;
}

.card{
  background:white;
  padding:25px;
  border-radius:18px;
  box-shadow:0 10px 25px rgba(0,0,0,.05);
}

.card h2{
  font-size:32px;
}

.card span{
  color:#64748b;
}
</style>