<!-- tableau de villes -->

<template>
  <div>
    <table class="table table-bordered table-sm table-hover">
      <thead>
        <tr>
          <th>Nom</th>
          <th>Population</th>  
        </tr>
      </thead>
      <tbody>
        <tr v-for="city in cities" :key="city.id">
          <td>{{ city.name }}</td>
          <td>{{ city.population }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
const props = defineProps({
  cities: {
    type: Array,
    required: true,
  },
});
</script>
