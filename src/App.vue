<template>
  <v-app>
    <v-app-bar
      color="orange darken-3"
      density="compact">
      <v-app-bar-title id="titre">Bienvenue chez Mouhamed. Vous pouvez utiliser le frigo à volonté</v-app-bar-title>
      <v-btn to="/">Home</v-btn>
    </v-app-bar>

    <v-main>
      <v-btn v-if="$route.path === '/'"
             id="ouvre"
             to="/PageFrigo">Ouvrir
      </v-btn>
      <v-container :class="{ 'home-page': $route.path === '/' }">
        <!-- les "composant view" s'afficheront ici -->
        <router-view/>
      </v-container>
    </v-main>
  </v-app>
</template>

<style scoped>
.page {
  min-height: 100vh;
  text-align: center;
}

.home-page {
  min-height: 100vh;
  text-align: center;
  background-image: url('../src/img/frigo-dans-le-salon.webp');
  background-size: cover;
  background-position: center;
}

#ouvre{
  border-radius: 50px;
  width: 10%;
  position : absolute;
  top: 40%;
  left: 15%;

  cursor: pointer;
}

#titre {
  text-align: center;
}

</style>
<script setup>
</script>
