<template>
  <div>
    <h2>Destaques dos Usuários</h2>
    <div>
      <h3>Primeiros Usuários</h3>
      <ul>
        <li v-for="user in firstUsers" :key="user.id">
          {{ user.name }} ({{ user.followers }} seguidores)
        </li>
      </ul>

      <h3>Usuários Recentes</h3>
      <ul>
        <li v-for="user in recentUsers" :key="user.id">
          {{ user.name }} ({{ user.followers }} seguidores)
        </li>
      </ul>

      <h3>Usuários Populares</h3>
      <ul>
        <li v-for="user in popularUsers" :key="user.id">
          {{ user.name }} ({{ user.followers }} seguidores)
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import usersData from '../data/thefuck-sample-100.json';

export default {
  name: 'UserHighlights',
  data() {
    return {
      firstUsers: [],
      recentUsers: [],
      popularUsers: [],
    };
  },
  mounted() {
    this.getUserHighlights();
  },
  methods: {
    getUserHighlights() {
      // Ordena e filtra os usuários
      this.firstUsers = usersData.slice(0, 5); // Primeiros 5
      this.recentUsers = [...usersData].reverse().slice(0, 5); // Últimos 5
      this.popularUsers = [...usersData]
        .sort((a, b) => b.user.followers - a.user.followers)
        .slice(0, 5); // Top 5 em seguidores
    },
  },
};
</script>

<style scoped>
/* Estilos específicos dos destaques de usuários */
</style>