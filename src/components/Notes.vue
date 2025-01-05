<template>
  <div class="card-container">
    <div v-for="note in notes" class="card" :key="note.Id" :style="{ backgroundColor: note.BackgroundColor }">
      <p class="main-text">{{ note.Text }}</p>
      <p class="date">{{ formatDate(note.Date) }}</p>
    </div>
  </div>
</template>

<script>
  import moment from 'moment';
  export default {
    name: 'Notes',
    props: {
      notes: Array
    },
    methods: {
      formatDate (dateString) {
        return moment(dateString).format('MM/DD/YYYY');
      }
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
