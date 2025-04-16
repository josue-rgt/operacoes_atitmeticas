<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    numOne: 0,
    numTwo: 0,
    oper: 'adicao',
    resp: ''
  })

  function getValueOne(e) {
    estado.numOne = e.target.value

    if(estado.numOne === '') {
      estado.numOne = 0
    }
    calc()
  }

  function getValueTwo(e) {
    estado.numTwo = e.target.value

    if(estado.numTwo === '') {
      estado.numTwo = 0
    }
    calc()
  }

  function getOperation(e) {
    estado.oper = e.target.value
    calc()
  }

  function calc() {
    const num1 = Number(estado.numOne)
    const num2 = Number(estado.numTwo)

    switch (estado.oper) {
      case 'adicao':
        estado.resp = num1 + num2
        break
      case 'subtracao':
        estado.resp = num1 - num2
        break
      case 'multiplicacao':
        estado.resp = num1 * num2
        break
      case 'divisao':
        if(num2 !== 0) {
          estado.resp = num1 / num2
        }else {
          estado.resp = 'Não é possivel dividir por ZERO'
        }
        break
    }
  }
</script>

<template>
  <div class="bg-light principal">
    <header>
      <nav class="navbar bg-dark p-4">
        <div class="container-fluid justify-content-center">
          <a class="navbar-brand text-light fs-2 fw-bold" href="#">
            <i class="bi bi-calculator me-2"></i>
            Operações Aritméticas
            <i class="bi bi-calculator ms-2"></i>
          </a>
        </div>
      </nav>
    </header>

    <section id="calcBack" class="container bg-dark p- rounded-4">
      <div class="row justify-content-between pt-5">
        <div class="col-4 ms-5 text-center">
          <label for="numberOne" class="form-label fw-bold text-light">Primeiro Número</label>
          <input @input="getValueOne" id="numberOne" type="number" class="form-control fw-bold text-center fs-3" placeholder="0">
        </div>
        <div class="col-2 text-center">
          <label for="operation" class="form-label fw-bold text-light">Operação</label>
          <select @change="getOperation" v-model="estado.oper" id="operation" class="form-select focus-ring focus-ring-danger form-control text-center fs-3 fw-bold" role="button">
            <option value="adicao" class="fs-5 fw-bold">+</option>
            <option value="subtracao" class="fs-5 fw-bold">-</option>
            <option value="multiplicacao" class="fs-5 fw-bold">*</option>
            <option value="divisao" class="fs-5 fw-bold">/</option>
          </select>
        </div>
        <div class="col-4 me-5 text-center">
          <label for="numberTwo" class="form-label fw-bold text-light">Segundo Número</label>
          <input @input="getValueTwo" id="numberTwo" type="number" class="form-control fw-bold text-center fs-3" placeholder="0">
        </div>
      </div>
      <div class="col pt-5 pb-5 ms-5 me-5 text-center d-block">
        <label for="result" class="form-label fw-bold text-light">Resultado</label>
        <input :value="estado.resp" id="result" class="focus-ring focus-ring-success form-control fw-bold text-center fs-3" placeholder="0">
      </div>
    </section>
  </div>
</template>

<style scoped>
  .principal {
    height: 100vh;
  }

  #calcBack {
    width: 700px;
    margin-top: 100px;
  }
 
  #result {
   cursor: default;
   pointer-events: none ;
  }
</style>
