<script setup>
import { reactive } from 'vue';
import inputNumber from './components/ImputNumber.vue';

const estado = reactive({
  numero1: "",
  numero2: "",
  operacao: "soma",
  resultado: ""
});

function calcular() {
  const num1 = parseFloat(estado.numero1);
  const num2 = parseFloat(estado.numero2);

  if (isNaN(num1) || isNaN(num2)) {
    estado.resultado = "Preencha ambos os campos com números válidos";
    return estado.resultado;
  }

  switch (estado.operacao) {
    case "soma":
      estado.resultado = (num1 + num2).toFixed(2); // Arredonda para duas casas decimais
      break;
    case "subtracao":
      estado.resultado = (num1 - num2).toFixed(2);
      break;
    case "multiplicacao":
      estado.resultado = (num1 * num2).toFixed(2);
      break;
    case "divisao":
      estado.resultado = (num1 / num2).toFixed(2);
      break;
  }

  return estado.resultado;
}
</script>

<template>
  <div class="container">
    <header>
      <h1 class="p-5 bg-light text-center mt-4 rounded">Calculadora Aritmética</h1>
    </header>
    <form>
      <div class="row pt-4">
        <div class="col-md-4">
          <inputNumber type="number" step="any" @input="evento => estado.numero1 = evento.target.value" />
        </div>
        <div class="col-md-2">
          <select class="form-control text-center" @change="evento => estado.operacao = evento.target.value">
            <option value="soma" selected>+</option>
            <option value="subtracao">-</option>
            <option value="multiplicacao">*</option>
            <option value="divisao">/</option>
          </select>
        </div>
        <div class="col-md-4">
          <inputNumber type="number" step="any" @input="evento => estado.numero2 = evento.target.value" />
        </div>
      </div>
    </form>
    <div class="row pt-4 justify-content-center">
      <p class="text-center fs-2">Solução</p>
      <div class="col-md-4 text-center border p-3 rounded fs-3 overflow-hidden">
        {{ calcular() }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 400px;
  margin: 0 auto;
}

header {
  text-align: center;
}

form {
  margin-top: 20px;
}

inputNumber {
  width: 100%;
  padding: 8px;
  font-size: 16px;
}

select {
  width: 100%;
  padding: 8px;
  font-size: 16px;
}

.border {
  border: 1px solid #dee2e6;
}

.fs-2 {
  font-size: 1.5rem;
}

.fs-3 {
  font-size: 1.25rem;
}
</style>
