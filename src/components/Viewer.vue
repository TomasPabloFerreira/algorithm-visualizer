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
      <option value="1">Burbuja</option>
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
        newElements.push({
          value: rand,
          height: rand + "px",
          color: "#6DB3A7"
        });
      }
      // Delete this when height fixed
      if (newElements[16] != "undefined")
        newElements[16] = {
          value: 500,
          height: 500 + "px",
          color: "#6DB3A7"
        };

      this.elements = newElements;
    },
    sort: function() {
      let sortingMethod = parseInt(this.sortingMethod);
      switch (sortingMethod) {
        case 0:
          this.selectionSort();
          break;
        case 1:
          this.bubbleSort();
          break;
        default:
          alert("Método no disponible");
          break;
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

    changeColor: function(color, a) {
      if (color == 0) {
        this.elements[a].color = "#6DB3A7";
      } else {
        this.elements[a].color = "#B3745B";
      }
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

        this.changeColor(1, i);
        this.changeColor(1, min);
        await new Promise(r => setTimeout(r, 200));
        this.swap(i, min);
        await new Promise(r => setTimeout(r, 200));
        this.changeColor(0, i);
        this.changeColor(0, min);
      }
    },
    bubbleSort: async function() {
      let arrayLength = this.elements.length;
      let sorted = false;
      while (!sorted) {
        sorted = true;
        for (let i = 0; i < arrayLength; i++) {
          this.changeColor(1, i);
          await new Promise(r => setTimeout(r, 200));
          this.changeColor(0, i);

          if (
            this.elements[i] != "undefined" &&
            this.elements[i].value > this.elements[i + 1].value
          ) {
            sorted = false;
            this.swap(i, i + 1);
          }
        }
        alert(sorted);
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
  border: 3px solid #b3745b;
  background-color: #ffcab5;
  position: relative;
  overflow-x: hidden;
  overflow-y: auto;
}

#sortingMethodLabel {
  margin-right: 0.2%;
}
</style>
