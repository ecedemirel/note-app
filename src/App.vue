<template>
  <main>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <new-note @add-note="addNote" v-if="showModal" v-model:showModal="showModal"></new-note>
      <notes :notes="notes"></notes>
    </div>
  </main>
</template>

<script>
  import NewNote from './components/NewNote.vue'
  import Notes from './components/Notes.vue'
  import axios from 'axios';

  export default {
    data () {
      return {
        showModal: false,
        notes: [],
      }
    },
    components: {
      newNote: NewNote,
      notes: Notes
    },
    methods: {
      getRandomColor () {
        const randomValue = () => Math.floor(Math.random() * 256);
        const r = randomValue();
        const g = randomValue();
        const b = randomValue();

        const mixRatio = 0.7;
        const pastelR = Math.min(255, Math.floor(r + (255 - r) * mixRatio));
        const pastelG = Math.min(255, Math.floor(g + (255 - g) * mixRatio));
        const pastelB = Math.min(255, Math.floor(b + (255 - b) * mixRatio));

        const toHex = (value) => value.toString(16).padStart(2, '0');
        const hexColor = `#${ toHex(pastelR) }${ toHex(pastelG) }${ toHex(pastelB) }`;

        return hexColor;
      },
      async getNotes () {
        try {
          const response = await axios.get('http://localhost:3000/api/notes');
          this.notes = response.data;
        } catch(error) {
          console.error('Error fetching notes:', error);
        }
      },
      async addNote (newNote) {
        const backgroundColor = this.getRandomColor();
        try {
          const response = await axios.post('http://localhost:3000/api/notes', { text: newNote, backgroundColor: backgroundColor });
          this.notes.push({
            id: response.data.id,
            text: response.data.text,
            date: new Date(response.data.date),
            backgroundColor: response.data.backgroundColor
          });
          this.showModal = false;
          this.getNotes()
        } catch(error) {
          console.error('Error adding note:', error);
        }
      },
    },
    mounted () {
      this.getNotes();
    }
  }
</script>

<style scoped>
  main {
    height: 100vh;
    width: 100vw;
  }

  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 100%;
    color: white;
    font-size: 20px;
  }
</style>