<template>
  <div class="viewer">
    <h1>Visor de algoritmos de ordenamiento</h1>
    <label for="elementsCount">Cantidad de elementos: </label>
    <br />
    <input type="number" id="elementsCount" v-model="elementsCount" />
    <button @click="generateRandomElements">Generar</button>
    <br />
    <br />
    <label for="sortingMethod" id="sortingMethodLabel">Algoritmo:</label>
    <select id="sortingMethod" v-model="sortingMethod">
      <option value="0">Burbuja</option>
      <option value="1">Otro</option>
      <option value="2">Otro</option>
      <option value="3">Otro</option>
    </select>
    <br><br><hr>
    <button @click="sort">Ordenar</button>
    <br>
    <hr>
    <div id="bars">
      <bars :elements="elements" :width="100 / elements.length + '%'"> </bars>
    </div>
  </div>
</template>

<script>
import Bars from "./Bars.vue";

export default {
  name: "Viewer",
  components: {
    Bars
  },

  data: () => {
    return {
      elementsCount: 20,
      elements: [],
      sortingMethod: 0
    };
  },
  methods: {
    generateRandomElements: function() {
      let newElements = [];
      let rand;
      for (let i = 0; i < this.elementsCount; i++) {
        rand = Math.floor(Math.random() * 501);
        newElements.push({ value: rand, height: rand + "px" });
      }
      // Delete this when height fixed
      if (newElements[16] != "undefined")
        newElements[16] = { value: 500, height: 500 + "px" };

      this.elements = newElements;
    },
    sort: function() {
      switch(this.sortingMethod){
        case 0: this.bubbleSort();
        break;
        default: alert("default");
      }
    },
    bubbleSort: function() {
      alert("bubble sort");
    }
  },
  mounted: () => {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#bars {
  /*:gradient="['#6fa8dc', '#42b983']"*/
  width: 90%;
  min-height: 500px;
  margin: 2% auto;
  border: 3px solid #6DB3A7;
  background-color: #FFCAB5;
  position: relative;
  overflow-x: hidden;
  overflow-y: auto;
}

#sortingMethodLabel {
  margin-right: 0.2%;
}
</style>
