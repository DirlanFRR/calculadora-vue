

<script setup>

import { reactive } from 'vue';

 const estado = reactive({
    numero1: "",
    numero2: "",
    operacao: "soma",
    resultado: ""
  })

  function calcular() {
    switch (estado.operacao) {
      case "soma":
        estado.resultado = parseFloat(estado.numero1) + parseFloat(estado.numero2);
        return estado.resultado;
      case "subtracao":
        estado.resultado = parseFloat(estado.numero1) - parseFloat(estado.numero2);
        return estado.resultado;
      case "multiplicacao":
        estado.resultado = parseFloat(estado.numero1) * parseFloat(estado.numero2);
        return estado.resultado;
      case "divisao":
        estado.resultado = parseFloat(estado.numero1) / parseFloat(estado.numero2);
        return estado.resultado;
    }
  }
</script>

<template>
   <div class="container">
    <header>
      <h1 class="p-5 bg-light text-center mt-4 rounded">Calculadora Aritmética</h1>
    </header>
    <form>
      <div class="row pt-4">
        <inputNumber @keyup="evento => estado.numero1 = evento.target.value" />
        <div class="col-md-2">
          <select class="form-control text-center" @change="evento => estado.operacao = evento.target.value">
            <option value="soma" selected>+</option>
            <option value="subtracao">-</option>
            <option value="multiplicacao">*</option>
            <option value="divisao">/</option>
          </select>
        </div>
        <div class="col">
          <inputNumber @keyup="evento => estado.numero2 = evento.target.value" />
        </div>
      </div>
    </form>
    <div class="row pt-4 justify-content-center">
      <p class="text-center fs-2">Solução</p>
      <div class="col-4 text-center border p-3 rounded fs-3 text-success text-end overflow-hidden">
        {{ calcular() }}
      </div>
    </div>
  </div>
 
</template>


<style scoped>
</style>

