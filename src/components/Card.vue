<template>
    <Card class="card">
      <template #header>
        <span class="p-card-header__name">{{ data.userName }}</span>
        <div class="p-card-header__icons">
          <i :class="['pi', {
            'pi-thumbs-up pi-thumbs-up--active': data.evaluation === 'liked',
            'pi-thumbs-down pi-thumbs-down--active': data.evaluation === 'desliked',
            'pi-thumbs-up': data.evaluation === 'neutral',
            }]">
          </i>
          <i class="pi pi-pencil"></i>
          <i class="pi pi-trash" @click="deleteCard(data.key)"></i>
        </div>
      </template>
      <template #content>
        <img class="p-card-content__picture" src="../assets/profilePicture.png" alt=""/>       
        <p class="p-card-content__note"> {{ data.text }} </p>
      </template>
      <template #footer>
        <div class="p-card-footer__line" />
        <div class="p-card-footer__info">
          <span class="p-card-footer__info__when"> {{ data.when }} </span>
          <span class="p-card-footer__info__date"> {{ data.date }} </span>
        </div>
      </template>
    </Card>  
</template>

<script>
import '../styles/components/card.scss'
import Card from 'primevue/card';

export default {
  components: {
    Card
  },
  props: {
    data: {
      type: Object,
      default: () => ({
        text: '“Candidato foi banido do processo”',
        when: 'Inserido na Triagem da vaga (47 - Operador de Máquina Industrial)',
        date: 'terça-feira, 13 de abril de 2021 13:29:10',
        userName: 'Pedro Ribeiro',
        evaluation: 'neutral',
        key: String,
  })
    }
  },

  methods: {
    deleteCard(key){
      this.$emit('delete-card', key)
    }
  }

}
</script>

<style>

</style>