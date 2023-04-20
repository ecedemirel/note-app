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

export default {
  data() {
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
    getRandomColor() {
      return "hsl(" + Math.random() * 360 + ", 100%, 75%)"
    },
    addNote(newNote) {
      this.notes.push({
        id: Math.floor(Math.random() * 1000000),
        text: newNote,
        date: new Date(),
        backgroundColor: this.getRandomColor()
      })
      this.showModal = false
    },
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