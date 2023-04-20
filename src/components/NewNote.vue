<template>
  <div class="overlay">
    <div class="modal">
      <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
      <p v-if="errorMessage">{{ errorMessage }}</p>
      <div class="button">
        <button @click="checkAndAdd">Add Note</button>
        <button class="close" @click="$emit('update:showModal', $event.target.value)">Close</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NewNote',
  props: {
    showModal: Boolean,
  },
  data() {
    return {
      newNote: '',
      errorMessage: ''
    }
  },
  methods: {
    checkAndAdd() {
      if (this.newNote === '') {
        return this.errorMessage = 'The note is required'
      }
      this.$emit('add-note', this.newNote)
    }
  },

  emits: ['add-note', 'update:showModal']
}
</script>

<style scoped>
.overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.77);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.button {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 1rem;
}

.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
  border-radius: 10px;
}

.modal .close {
  background-color: rgb(193, 15, 15);
}

.modal p {
  color: rgb(193, 15, 15);
}
</style>