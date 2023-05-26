<script setup>
import { reactive } from 'vue';

const estado = reactive({
  opcaoDeCalculo: 'adicao',
  sinal: '+',
  n1: '',
  n2: '',
  resultado: '',
})


function escolheSinal(opcao){
  switch(opcao) {
    case 'adicao':
      return estado.sinal = '+';
    case 'subtracao':
      return estado.sinal = '-';
    case 'multiplicacao':
      return estado.sinal = 'X';
    case 'divisao':
      return estado.sinal = '/';
  }
}

function escolheCalculo(e) {
estado.opcaoDeCalculo = e.target.value;
if (estado.n1 | estado.n2){
  estado.n1 = '';
  estado.n2 = '';
  estado.resultado = '';
}
}

function calcula(n1, n2, opcao){
  switch(opcao) {
    case 'adicao':
    return estado.resultado = n1 + n2;
    case 'subtracao':
    return estado.resultado = n1 - n2;
    case 'multiplicacao':
    return estado.resultado = n1 * n2;
    case 'divisao':
    return estado.resultado = n1 / n2;
  }
}
</script>

<template>
  <div class="container text-center">
    <div class="row d-flex justify-content-center mb-3">
      <h1 class="fw-bold">Calculadora</h1>
      <select @change="e => escolheCalculo(e)" class="form-select form-control w-75">
        <option value="adicao">Adição</option>
        <option value="subtracao">Subtração</option>
        <option value="multiplicacao">Multipliçao</option>
        <option value="divisao">Divisão</option>
      </select>
    </div>
    <div class="row">
      <form>
        <input @keyup="calcula(estado.n1, estado.n2, estado.opcaoDeCalculo)" v-model="estado.n1" class="form-control" type="number">
        <span class="fw-bold h3">{{ escolheSinal(estado.opcaoDeCalculo) }}</span>
        <input @keyup="calcula(estado.n1, estado.n2, estado.opcaoDeCalculo)" v-model="estado.n2" class="form-control" type="number">
        <div>
          <span class="fw-bold h3"> {{ `= ${estado.resultado}` }}</span>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped>
.container {
  border: 2px solid black;
  background-color: blanchedalmond;
  padding: 10px;
  max-width: 30%;
  width: 100%;
}

select,
input {
  text-align-last: center;
}

select {
  cursor: pointer;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>
