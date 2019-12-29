<template>
  <div class="bars">
    <div
      class="bar"
      v-for="(element, index) in elements"
      v-bind:key="index"
      v-bind:style="{
        height: element.height,
        width: width
      }"
    ></div>
  </div>
</template>

<script>
export default {
  name: "Bars",
  props: {
    elements: Array,
    width: String
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  padding: 0;
  margin: 0;
}

/*
  Change this div to a separated component.
  In computed set height = value + "px" 
*/
.bar {
  /* Position*/
  display: inline-block;
  background-color: #6DB3A7;
  max-height: 500px;
  overflow: hidden;

  /* Border */
  box-sizing: border-box;
  border: 1px solid rgb(133, 133, 133);
}
</style>
