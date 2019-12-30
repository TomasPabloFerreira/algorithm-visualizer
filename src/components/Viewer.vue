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
      <option value="0">Selección</option>
      <option value="1">Otro</option>
      <option value="2">Otro</option>
      <option value="3">Otro</option>
    </select>
    <br /><br />
    <hr />
    <button @click="sort">Ordenar</button>
    <br />
    <hr />
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
      switch (this.sortingMethod) {
        case 0:
          this.selectionSort();
          break;
        default:
          alert("default");
      }
    },
    swap: function(a, b) {
      let auxValue = this.elements[a].value;
      let auxHeight = this.elements[a].height;

      this.elements[a].value = this.elements[b].value;
      this.elements[b].value = auxValue;

      this.elements[a].height = this.elements[b].height;
      this.elements[b].height = auxHeight;
    },
    selectionSort: async function() {
      let arrayLength = this.elements.length;
      for (let i = 0; i < arrayLength; i++) {
        let min = i;
        for (let j = i + 1; j < arrayLength; j++) {
          if (this.elements[j].value < this.elements[min].value) {
            min = j;
          }
        }
        this.swap(i, min);
        await new Promise(r => setTimeout(r, 500));
      }
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
  border: 3px solid #6db3a7;
  background-color: #ffcab5;
  position: relative;
  overflow-x: hidden;
  overflow-y: auto;
}

#sortingMethodLabel {
  margin-right: 0.2%;
}
</style>
