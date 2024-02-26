<script setup>
import { defineProps } from 'vue';

const { produit, handlerAdd1, handlerDelete1 , handlerDelete} = defineProps(["produit", "handlerAdd1", "handlerDelete1", "handlerDelete"]);


</script>


<template>
  <div id="infoP">
    <img :src="produit.photo" style="width: 100px; height: 100px;" />
    <div id="nomP">
      {{ produit.nom }}
    </div>
    <div id="supP">
      <button name="boutonSuppr" class="bouton" @click="handlerDelete(produit.id)">
        <img src="../img/corbeille.png" alt="supprimerProduit" width="16"/>
      </button>
    </div>
    <div id="qteProduit">
      <button name="boutonMoins" class="bouton" @click="handlerDelete1(produit)">
        <img src="../img/moins.png" alt="moins" width="10" />
      </button>
      {{ produit.qte }}
      <button name="boutonPlus" class="bouton" @click="handlerAdd1(produit)">
        <img src="../img/plus.png" alt="plus" width="10" />
      </button>
    </div>

  </div>
  <br><br><br>


</template>


<style scoped>
#infoP{
  background-color: #ffff;

  top: 20%;
  left: 12%;
  height: 5em;
  width : 11em;

  border-radius: 15px;
  margin-bottom: 15%;

  padding: 15px 5px 0 5px;

  color: rgb(27,32,42) ;
  justify-content: center;

  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

#nomP{
  text-align: center;
  margin-top: 5%;
}

#optionP img{
  margin-right: 3px;
  margin-left: 3px;
}

#qteProduit{
  font-size: small;
}

button{
  border: transparent;
  border-radius: 15px;
}
</style>
