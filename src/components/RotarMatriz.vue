<template >
  <div class="container">
    <div class="d-flex align-items-center justify-content-center mt-5">
      <h6>JSON Matriz input:</h6>
      <input
        type="text"
        name="array"
        v-model="texto"
        placeholder="Ingrese matriz"
      />
      <button class="mx-3 btn btn-primary" @click="procesar()">Rotar</button>
    </div>
    <div class="d-flex flex-column align-items-center mt-5">
      <h4>Resultado:</h4>

      <table v-if="isMatriz" class="mt-3">
        <tr v-for="a in solution" :key="a">
          <td v-for="b in a" :key="b">{{ b }}</td>
        </tr>
      </table>
      <div v-else class="alert alert-danger mt-3" role="alert">
        <strong>El texto ingresado no es una matriz</strong> .
      </div>
    </div>
    <div class="mt-3">
      <ul class="list-group">
        <li class="list-group-item active" aria-current="true">Ejemplos</li>
        <li class="list-group-item">[ [1,2], [3,4] ]</li>
        <li class="list-group-item">[ [1,2,3], [4,5,6], [7,8,9] ]</li>
        <li class="list-group-item">[ [1,2,3,4], [5,6,7,8], [9,10,11,12], [13,14,15,16] ]</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "rotar-matriz",

  data() {
    return {
      texto: "", //Input value
      model2: [], // Arreglo auxiliar
      solution: [], //Arreglo con la matriz final
      isMatriz: true, // variable para mostrar el resultado o mensaje de error
    };
  },
  methods: {
    /*  Metodo donde se convierte el valor del input a un arreglo, 
        y se maneja el error si es que lo ingresado no es un arreglo
     */
    procesar() {
      try {
        this.model2 = JSON.parse(this.texto);
        this.rotar();
        this.isMatriz = true;
      } catch (error) {
        this.isMatriz = false;
      }
    },
    /* Metodo  para rotar la matriz NxN en sentido antihorario */
    rotar() {
      this.solution = this.model2.map((line, i) => {
        return line.map((cell, j) => {
          return this.model2[j][this.model2.length - 1 - i];
        });
      });
    },
  },
};
</script>

<style scoped >
table,
th,
td {
  border: 1px solid;
  width: 10%;
  text-align: center;
  border-collapse: collapse;
  padding: 1rem;
  caption-side: top;
}
</style>