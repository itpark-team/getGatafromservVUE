<template>
  <ul>
    <li v-for="car in cars" :key="car.model">
      {{ car.model }} | {{ car.power }}
    </li>
  </ul>
  <button @click="loadJsonData">loadJsonData</button>
</template>

<script>
export default {
  name: "ComponentOne",
  data() {
    return {
      cars: []
    }
  },
  methods: {
    loadJsonData() {
      fetch('http://localhost:8090/cars', {
        method: 'get',
        headers: {
          'Content-type': 'application/json'
        },
      }).then(response => response.json()).then(responseAsObject => {
        this.cars = responseAsObject.cars
        console.dir(this.cars)
      }).catch(error => {
        console.log('Looks like there was a problem: \n', error);
      });
    }
  }
}
</script>

<style scoped>

</style>