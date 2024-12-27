<template>
  <div id="app">
    <b-navbar toggleable="lg" class="custom-navbar">
      <b-navbar-brand>Cursos AlfaWeb</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item href="/"><b-icon icon="house-door-fill"></b-icon></b-nav-item>
          <b-nav-item href="/admin"><b-icon icon="wrench"></b-icon></b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.custom-navbar {
  background-color: #6a1b9a;
  color: white;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  justify-content: space-between;
}

.custom-navbar .navbar-nav .nav-link {
  color: white;
}

.custom-navbar .navbar-brand {
  color: white;
}
</style>