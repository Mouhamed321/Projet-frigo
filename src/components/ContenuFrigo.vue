<script setup>
import {onMounted, reactive} from "vue";
import Produit from "../Produit.js";
import ItemProduit from "../components/ItemProduit.vue";
import AjoutProduit from "@/components/AjoutProduit.vue";
import RechercheProduit from "@/components/RechercheProduit.vue";


const listeProduits = reactive([]);
const rechercheProduit =reactive([]);
const url = "https://webmmi.iut-tlse3.fr/~pecatte/frigo/public/10/produits"


//fonction pour charger les produits du frigo
function chargerProduit() {
  const fetchOptions = { method: "GET" };
  fetch(url, fetchOptions)
    .then((response) => { return response.json();})
    .then((dataJSON) => {
      listeProduits.splice(0, listeProduits.length)
      dataJSON.forEach((produit) => {
        listeProduits.push(new Produit(produit.id, produit.nom, produit.qte, produit.photo))})
    })
    .catch((error) => console.log(error));
  console.log(listeProduits)
}

onMounted(() => {
  chargerProduit();
})

//fonction pour supprimer un produit

function handlerDelete(id) {
  console.log(id);
  const fetchOptions = {
    method: "DELETE",
  };
  fetch(url + "/" + id, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      chargerProduit();
    })
    .catch((error) => console.log(error));
}

//fonction qui réduit la qté du produit
function handlerDelete1(produit) {
  produit.reduireQte();
  if (produit.qte < 1) { handlerDelete(produit.id); // si qté = 1 et qu'on réduit, le produit est supprimer du frigo
  } else {
    let myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");
    const fetchOptions = {
      method: "PUT",
      headers: myHeaders,
    };
    fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        chargerProduit();
      })
      .catch((error) => console.log(error));
  }
}

//fonction qui augmente la qté du produit
function handlerAdd1(produit) {
  produit.augmenterQte();
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  const fetchOptions = {
    method: "PUT",
    headers: myHeaders,
  };
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      chargerProduit();
    })
    .catch((error) => console.log(error));
}


//fonction pour ajouter un produit au frigo

function handlerAdd(nom, qte, photo) {
  console.log(nom);
  console.log(qte);
  console.log(photo);

  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");

  const fetchOptions = {
    method: "POST",
    headers: myHeaders,
    body: JSON.stringify({ nom: nom, qte: qte, photo: photo }),
  };
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      chargerProduit();
    })
    .catch((error) => {
      console.error(error);
    });
}


//fonction rechercher un produit

function handlerSearch(saisie) {
  /* on récupère le mot clé nécessaire à la recherche */
  const fetchOptions = { method: "GET" };

  fetch(url + "?search=" + saisie, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      let produitrechercher = dataJSON;
      document.getElementById("recherche").innerHTML += "<ul>";
      for (let produit of produitrechercher) {

        document.getElementById("recherche").innerHTML +=
          "Qté: " + produit.qte +
          "<br>" +
          "<img src='" + produit.photo + "' alt='Photo du produit' style=\"width: 100px; height: 100px;\">";
      }
      document.getElementById("recherche").innerHTML += "</ul>";
    })
    .catch((error) => console.log(error));
}



</script>

<template>
  <div id="page">
    <div>
      <h3 class="titre1">Contenu du frigo</h3><br><br><br>
      <v-row dense>
        <!-- Boucle pour afficher les cartes produits -->
        <ItemProduit v-for="produit in listeProduits"
                     :key="produit.id"
                     :produit="produit"
                     :handlerDelete1="handlerDelete1"
                     :handlerAdd1="handlerAdd1"
                     :handlerDelete="handlerDelete"
        />

      </v-row>

    </div>
    <v-row dense>
      <AjoutProduit :handlerAdd="handlerAdd"/>
      <RechercheProduit @Search="handlerSearch" />
    </v-row>
  </div>



</template>


<style scoped>
.titre1 {
  font-size: 30px;
  font-family: "Times New Roman", Times, serif;
  color: #f5733b;
  margin-left: 20px; /* Ajustez cette valeur selon votre besoin */
}



</style>

