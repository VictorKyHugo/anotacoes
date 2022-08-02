<template>
  <div class="notes">
    <NoteInput @new-note="addNewNote($event)" />
    <div class="notes__note"  v-for="note in notesToRender" :key="note.key">
      <Card 
        :data="note" 
        @delete-card="deleteNote($event)"
        @edit-card="editNote($event)"
      />
    </div>
    <Paginator 
      class="notes__paginator" 
      @page="getCurrentPageData($event)" 
      :first="currentPageFirstItemIndex" 
      :rows="rowsPerPage" 
      :totalRecords="notes.length" 
    />
  </div>
</template>

<script>
import '../styles/pages/notes.scss'
import Card from '../components/Card.vue'
import NoteInput from '../components/NoteInput.vue'
import Paginator from 'primevue/paginator';

export default {
  components: {
    Card,
    Paginator,
    NoteInput,
},
  data() {
    return {
      notesToRender: [],
      rowsPerPage: 3,
      currentPageFirstItemIndex: 0,
      notes: [
        {
          text: '“Candidato foi banido do processo”',
          when: 'Inserido na Triagem da vaga (47 - Operador de Máquina Industrial)',
          date: 'terça-feira, 13 de abril de 2021 13:29:10',
          userName: 'Pedro Ribeiro',
          evaluation: 'neutral',
          key: 0
        },
        {
          text: '“Candidato não tem perfil. Mas foi identificado que é talento para Gestor.”',
          when: 'Inserido na Triagem da vaga (47 - Operador de Máquina Industrial)',
          date: 'terça-feira, 13 de abril de 2021 13:29:10',
          userName: 'Rodrigo Machado',
          evaluation: 'desliked',
          key: 1
        },
        {
          text: '“Candidato foi banido do processo”',
          when: 'Inserido na Triagem da vaga (47 - Operador de Máquina Industrial)',
          date: 'terça-feira, 13 de abril de 2021 13:29:10',
          userName: 'Rafael Andrade',
          evaluation: 'liked',
          key: 2
        },
        {
          text: '“Candidato foi banido do processo”',
          when: 'Inserido na Triagem da vaga (47 - Operador de Máquina Industrial)',
          date: 'terça-feira, 13 de abril de 2021 13:29:10',
          userName: 'Pedro Ribeiro',
          evaluation: 'desliked',
          key: 3
        },
      ]
    };
  },

  methods: {
    getCurrentPageData({ first }) {
      this.notesToRender = this.notes.slice(first, first + this.rowsPerPage)

      this.currentPageFirstItemIndex = first
    },

    deleteNote(key){
      this.notes = this.notes.filter(item => item.key !== key)
      this.getCurrentPageData({ first: this.currentPageFirstItemIndex })
    },

    editNote({key, text}){
      const noteIndex = this.notes.findIndex(note => note.key === key)
      this.notes[noteIndex].text = `“${text}”`
    },

    addNewNote(data){
      const newNoteKey =  this.notes.length ? this.notes[this.notes.length - 1].key + 1 : 0

      const newNote = {
          text: data.text,
          when: data.when,
          date: data.date,
          userName: data.userName,
          evaluation: data.evaluation,
          key: newNoteKey
      }

      this.notes = [...this.notes, newNote]
      this.getCurrentPageData({ first: this.currentPageFirstItemIndex })
    }
  },

  mounted(){
    this.getCurrentPageData({first: this.currentPageFirstItemIndex})
  }
}
</script>

<style>

</style>