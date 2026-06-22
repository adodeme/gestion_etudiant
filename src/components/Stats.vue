<script setup>
defineProps({
  total: Number
})
</script>

<template>
  <div class="stats">
    <div class="card">
      <h2>{{ total }}</h2>
      <span>Étudiants</span>
    </div>
  </div>
</template>

<style scoped>
.stats{
  margin-bottom:25px;
}

.card{
  width:220px;
  background:white;
  padding:25px;
  border-radius:18px;
  box-shadow:0 10px 25px rgba(0,0,0,.05);
}

.card h2{
  font-size:36px;
}

.card span{
  color:#64748b;
}
</style>