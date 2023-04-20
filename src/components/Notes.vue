<template>
  <div class="card-container">
    <div v-for="note in notes" class="card" :key="note.id" :style="{ backgroundColor: note.backgroundColor }">
      <p class="main-text">{{ note.text }}</p>
      <p class="date">{{ note.date.toLocaleDateString("en-EN") }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Notes',
  props: {
    notes: Array
  }
}
</script>

<style scoped>
.card {
  width: 210px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 12px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 10px;
  margin-bottom: 15px;
  text-align: justify;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
}

.card-container .date {
  display: flex;
  justify-content: flex-end;
  font-weight: bold;
}
</style>
