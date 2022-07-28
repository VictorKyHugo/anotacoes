<template>
  <div class="container">
    <Notes />
  </div>
</template>

<script>

import '../src/styles/utilities/global.scss'
import Notes from '../src/pages/Notes.vue'

export default {
  components: {
    Notes
  },

};
</script>

<style scoped>
  .container{
    background-color: #F8F9FA;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>