<template>
  <div class="viewer">
    <div class="conteiner-fluid">
      <form action="#">
        <div class="form-row">
          <div class="form-group col-md-4 offset-4">
            <label for="elementsCount">Cantidad de elementos: </label>
            <input
              type="number"
              id="elementsCount"
              v-model="elementsCount"
              class="form-control"
            />
          </div>
        </div>

        <div class="form-row">
          <div class="col">
            <button
              @click="generateRandomElements"
              class="btn btn-primary mb-2"
            >
              Generar
            </button>
          </div>
        </div>

        <hr />

        <div class="form-row">
          <div class="form-group col-md-4 col-sm-12 offset-4">
            <label for="sortingMethod" id="sortingMethodLabel"
              >Algoritmo:</label
            >
            <select
              id="sortingMethod"
              v-model="sortingMethod"
              class="form-control"
            >
              <option value="0">Selección</option>
              <option value="1">Burbuja</option>
              <option value="2">Inserción</option>
              <option value="3">Otro</option>
            </select>
          </div>
        </div>

        <div class="form-row">
          <div class="col">
            <div class="form-check">
              <input
                type="checkbox"
                id="showIteration"
                v-model="showIteration"
                class="form-check-label mr-2"
              />
              <label for="showIteration" class="form-check-label"
                >Mostrar iteraciones</label
              >
            </div>
          </div>
        </div>
      </form>

      <button @click="sort" class="btn btn-success mt-3">Ordenar</button>

      <div id="bars">
        <bars :elements="elements" :width="100 / elements.length + '%'"> </bars>
      </div>
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
      elementsCount: 200,
      elements: [],
      sortingMethod: 0,
      showIteration: true
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
      if (newElements[16] != "undefined" && newElements[16] != null) {
        newElements[16] = {
          value: 500,
          height: 500 + "px",
          color: "#6DB3A7"
        };
      } else {
        newElements[0] = {
          value: 500,
          height: 500 + "px",
          color: "#6DB3A7"
        };
      }

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
        case 2:
          this.insertionSort();
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
          if (this.showIteration) {
            this.changeColor(1, j);
            await new Promise(r => setTimeout(r, 1));
            this.changeColor(0, j);
          }
          if (this.elements[j].value < this.elements[min].value) {
            this.changeColor(1, j);
            this.changeColor(0, min);
            min = j;
          }
        }

        this.changeColor(1, i);
        this.changeColor(1, min);
        await new Promise(r => setTimeout(r, 50));
        this.swap(i, min);
        await new Promise(r => setTimeout(r, 50));
        this.changeColor(0, i);
        this.changeColor(0, min);
      }
    },
    bubbleSort: async function() {
      let arrayLength = this.elements.length;
      var sorted = false;
      while (!sorted) {
        sorted = true;
        for (let i = 0; i < arrayLength - 1; i++) {
          if (this.elements[i].value > this.elements[i + 1].value) {
            sorted = false;
            this.swap(i, i + 1);
          }
          if (this.showIteration) {
            this.changeColor(1, i);
            await new Promise(r => setTimeout(r, 1));
            this.changeColor(0, i);
          } else if (i == arrayLength - 2) {
            this.changeColor(1, i + 1);
            await new Promise(r => setTimeout(r, 50));
            this.changeColor(0, i + 1);
          }
        }
        arrayLength--;
      }
    },
    insertionSort: async function() {
      let arrayLength = this.elements.length;
      for (let i = 1; i < arrayLength; i++) {
        let j = i - 1;
        let tmpValue = this.elements[i].value;
        let tmpHeight = this.elements[i].height;
        while (j >= 0 && this.elements[j].value > tmpValue) {
          if (this.showIteration) {
            this.changeColor(1, j);
            await new Promise(r => setTimeout(r, 1));
            this.changeColor(0, j);
          }

          this.elements[j + 1].value = this.elements[j].value;
          this.elements[j + 1].height = this.elements[j].height;
          j--;
        }
        this.elements[j + 1].value = tmpValue;
        this.elements[j + 1].height = tmpHeight;

        this.changeColor(1, j + 1);
        await new Promise(r => setTimeout(r, 50));
        this.changeColor(0, j + 1);
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
