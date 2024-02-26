<script setup>

defineEmits(["Search"]);

</script>

<template>
  <div class="container">
    <h2 id="titre1">Rechercher un produit</h2>
    <form @submit.prevent="$emit('Search', saisie)" id="recherche">
      <div class="form-group">
        <label for="recherche">Nom du produit:</label>
        <input type="text" v-model="saisie"  class="form-control" required>
      </div>
      <button type="submit" id="bouton" class="btn btn-primary">Rechercher</button>
    </form>
  </div>

</template>

<style scoped>
.container {
  max-width: 400px;
  margin: 0 auto;
}

.form-group {
  margin-bottom: 15px;
}

.form-control {
  width: 100%;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.btn {
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  border-radius: 4px;
  background-color: #5df122;
  color: #fff;
  cursor: pointer;
}

.btn-primary {
  background-color: #5df122;
}

.btn-primary:hover {
  background-color: #5df122;
}

#titre1 {
  font-size: 30px;
  font-family: "Times New Roman", Times, serif;
  color: #f5733b;
  margin-left: 20px; /* Ajustez cette valeur selon votre besoin */
}

</style>
