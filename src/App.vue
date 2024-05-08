<script setup>
  import { reactive } from "vue";

  const state = reactive({
    firstNum: '',
    secondNum: '',
    selectOperation: 'add',
    operations: {
      add: (a, b) => a + b,
      subtraction: (a, b) => a - b,
      multi: (a, b) => a * b,
      divi: (a, b) => (b == 0 ? 'Divisão por zero' : a/b),
    },
    result: 0
  });


  const getResult = () => {
    const {firstNum, secondNum, selectOperation} = state;

    const castFirstNum = parseFloat(firstNum);
    const castSecondNum = parseFloat(secondNum);

    state.result = state.operations[selectOperation](castFirstNum, castSecondNum);
  }
</script>



<template>
  <div class="container p-5">

    <header class="text-center m-4">
      <h1 class="display-3 fw-medium">Calculadora Simples</h1>
    </header>


    <form class="d-flex flex-column justify-content-center align-items-center">
      <div class="row m-2">
        <label class="col-md-6">Insira um número:</label>
        <input
          v-model="state.firstNum" 
          @input="getResult" 
          class="col-md-6 form-control" 
          type="number"
        >
      </div>

      <div class="row m-2">
        <label class="col-md-6">Insira um número:</label>
        <input 
          v-model="state.secondNum" 
          @input="getResult" 
          class="col-md-6 form-control" 
          type="number"
        >
      </div>

      <div class="row col-md-2 m-3 text-center form-floating">
        <select 
          v-model="state.selectOperation" 
          @change="getResult"
          class="form-select" 
          id="floatingSelect" 
          aria-label="Escolha a operação"
        >
          <option value="add">Soma</option>
          <option value="subtraction">Subtração</option>
          <option value="multi">Multiplicação</option>
          <option value="divi">Divisão</option>
        </select>
        <label for="floatingSelect">Escolha a operação</label>
      </div>
    </form>


    <div class="text-center fs-1">
      <p>{{ !state.result? 0 : state.result }}</p>
    </div>
    
  </div>
</template>




<style scoped>

</style>