<template>
  <header class="text-center bg-blue-800 text-white p-4 mb-10">
    <nav>
      <router-link to="/">Tableau de bord</router-link> |
      <router-link to="/add">Ajouter un syst&egrave;me</router-link>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'Header',
};
</script>
