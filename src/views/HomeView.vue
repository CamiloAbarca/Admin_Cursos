<template>
  <div>
    <br>
    <h1>Lista de Cursos</h1>
    <HomeComponent></HomeComponent>
  </div>
</template>

<script>
import HomeComponent from '@/components/Home.vue'

export default {
  name: 'HomeView',
  components: {
    HomeComponent
  }
}
</script>
