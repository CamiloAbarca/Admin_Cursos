<template>
  <div>
    <br>
    <h1>Administración</h1>
    <AgregarComponent></AgregarComponent>
    <AdminComponent></AdminComponent>
    <TotalComponent></TotalComponent>
  </div>
</template>

<script>
import AdminComponent from '@/components/Admin.vue'
import TotalComponent from '@/components/Total.vue'
import AgregarComponent from '@/components/Agregar.vue'

export default {
    name: 'AdminView',
    components: {
      AdminComponent,
      TotalComponent,
      AgregarComponent
    }

}
</script>

<style>

</style>