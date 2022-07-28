<template>
    <div class="note-input">
        <div class="note-input__header">
            <img class="note-input__header__picture" src="../assets/profilePicture.png" alt=""/>       
            <Textarea 
              class="note-input__header__input" 
              :autoResize="true"  
              v-model="text" 
              placeholder="Anotações sobre o participante..."
              @keyup.enter="emitNote()"
            />
        </div>

        <div class="note-input__footer">
            <div class="note-input__footer__icons">
                <i @click="setPositiveNote" :class="['pi pi-thumbs-up', {'pi-thumbs-up--active': evaluation === 'liked'}]"></i>
                <i @click="setNegativeNote" :class="['pi pi-thumbs-down', {'pi-thumbs-down--active': evaluation === 'desliked'}]"></i>
            </div>
            <Button @click="emitNote" class="note-input__footer__button">Inserir Anotação</Button>
        </div>
    </div>
</template>

<script>
import '../styles/components/noteInput.scss'
import Textarea from 'primevue/textarea';
import Button from 'primevue/button';

export default {
  components: {
    Textarea,
    Button
  },
  data() {
    return {
      text: "",
      evaluation: "neutral",
      data: {}
    };
  },

  methods: {

    reset(){
      this.text = "",
      this.evaluation = "neutral"
    },

    setPositiveNote(){
      switch (this.evaluation) {
        case 'neutral':
          this.evaluation = 'liked'
          break;
        case 'liked': 
          this.evaluation = 'neutral'
          break;
        case 'desliked':
          this.evaluation = 'liked'
          break;
      }

    },
    setNegativeNote(){
      switch (this.evaluation) {
        case 'neutral':
          this.evaluation = 'desliked'
          break;
        case 'desliked': 
          this.evaluation = 'neutral'
          break;
        case 'liked':
          this.evaluation = 'desliked'
          break;
      }
    },

    getDateNow(){
      const weekList = ["Domingo", "Segunda-Feira", "Terça-Feira", "Quarta-Feira", "Quinta-Feira", "Sexta-Feira", "Sábado"];
      const monthList = ["Janeiro", "Fevereiro", "Março", "Abril", "Maio", "Junho", "Julho", "Agosto", "Setembro", "Outubro", "Novembro", "Dezembro"]

      const date = new Date().toLocaleDateString('pt-BR')
      const time = new Date().toLocaleTimeString('pt-BR')

      const [day, month, year] = (date.split('/'))

      const monthNumber = month.substring(0, 1) === '0' ? month.substring(1) : month
      const weekDay = weekList[new Date().getDay()]
      const monthName = monthList[monthNumber - 1]

      return `${weekDay}, ${day} de ${monthName} de ${year} ${time}`
    },

    getNoteData(){
      this.getDateNow()

      this.data = {
        text: `“${this.text}”`,
        evaluation: this.evaluation,
        userName: 'Victor Hugo',
        when: 'Inserido na Triagem da vaga (47 - Operador de Máquina Industrial)',
        date: this.getDateNow()
      }
    },

    emitNote(){
      this.getNoteData()
      this.$emit('new-note', this.data)

      this.reset()
    }
  }
}
</script>

<style>

</style>