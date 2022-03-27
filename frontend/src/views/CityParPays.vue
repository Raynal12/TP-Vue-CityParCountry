<template>
<!-- body -->

    <div id="countries"> Tableau des Villes en fonction du Pays sélectionné </div>
    <hr>

    <!-- Le template Mustache qui sert à formater le sélecteur de pays -->

        <label for="countrySelector">Choisissez un pays</label>
        <!-- Quand on sélectionne un pays, on fait un appel AJAX pour afficher ses villes -->
        <select id="countrySelector" @input="fetchCities">
                <!-- La valeur de l'option est l'URL REST des villes du pays sélectionné -->
                <option 
                v-for="country in data.allCountries" 
                :key="country.id"
                :value  ="country._links.cities.href">{{country.name}}
               </option>
        </select>      <!-- /les labels et selects sont mieux en minusculs-->

        <!-- balise auto fermante tableau villes -->
        <TableauCity v-bind:cities = "data.allCities"/>


</template>








<script setup>
//mettre les get des API (villes et pays)

import {reactive, onMounted} from "vue";        //onMounted : quand on rafraichit la page, les fonctions sont appelées
import TableauCity from "@/components/TableauCity.vue";

//instaurer la variable réactive :
const data = reactive({
    allCountries : {}, //référence à touts les pays
    allCities : {}, //référence à toutes les villes
})


function refresh() {        // fonction qui prend tous les pays
  fetch("api/countries")
    .then((response) => {
      if (!response.ok) { // status != 2XX
        throw new Error(response.status);
      }
      return response.json();
    })
    .then((json) => {
      data.allCountries = json._embedded.countries;
    })
    .catch((error) => alert(error));
}

// Fait l'appel AJAX, puis montre les villes pour le pays sélectionné
function fetchCities() {
    fetch(document.getElementById("countrySelector").value)        //quand on prend la valeur du pays
        .then(response => response.json())
        .then(json => {         //on rajoute dans le tableau les villes
            data.allCities = [];
            let listVille = json._embedded.cities;      //prne d la liste des villes
            for (let i =0; i<listVille.length; i++) {
                data.allCities.push(listVille[i]);
            }
        })
        .catch(error => showError(error));
}



onMounted(() => {       // a chaque rafraichissement, les 2 fonctions sont appellées (l'API qui appelle les villes, les valeurs en fonction du selector)
    refresh();
    fetchCities();
})

</script>