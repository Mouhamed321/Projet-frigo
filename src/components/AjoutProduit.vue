<script setup>
import {defineProps, ref} from 'vue'
const { handlerAdd } = defineProps(["handlerAdd"]);

const nom = ref('');
const qte = ref('');
const photo = ref('');

const ajoutProduit = () => {
  handlerAdd(nom.value, qte.value, photo.value);
  nom.value = '';
  qte.value = '';
  photo.value = '';
};
</script>

<template>
  <div class="container">
    <h2 class="titre1">Ajouter un produit</h2>
    <form @submit.prevent="ajoutProduit" class="form">
      <div class="form-group">
        <label for="nom">Nom du produit:</label>
        <input type="text" id="nom" v-model="nom" class="form-control" required>
      </div>
      <div class="form-group">
        <label for="qte">Quantité:</label>
        <input type="number" id="qte" v-model.number="qte" class="form-control" required>
      </div>
      <div class="form-group">
        <label for="lienPhoto">Lien de la photo:</label>
        <input type="url" id="photo" v-model="photo" class="form-control" required>
      </div>
      <button type="submit" class="btn btn-primary">Ajouter</button>
    </form>
  </div>
</template>

<style>
.container {
  max-width: 400px;
  margin: 0 auto;
}

.form {
  margin-top: 20px;
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

.titre1 {
  font-size: 30px;
  font-family: "Times New Roman", Times, serif;
  color: #f5733b;
  margin-left: 20px; /* Ajustez cette valeur selon votre besoin */
}
</style>
