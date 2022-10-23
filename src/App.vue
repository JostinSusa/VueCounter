<script setup>
import { ref, computed } from "vue";

const counter = ref(0);

const arrayCounter = ref([]);

//Metodo
const changeCounter = (toggler) => {
  switch (toggler) {
    case 1:
      counter.value++;
      break;
    case 2:
      counter.value--;
      break;
    case 3:
      counter.value = 0;
      break;
  }
};

const addNumber = () => {
  arrayCounter.value.push(counter.value);
};

// computed
const classCounter = computed(() => {
  if (counter.value == 0) {
    return "text-info";
  } else if (counter.value > 0) {
    return "text-success";
  } else {
    return "text-danger";
  }
});

const validateCounterArray = computed(() => {
  if (arrayCounter.value.filter((item) => item == counter.value).length > 0) {
    return true;
  }
});
</script>

<template>
  <div class="text-center">
    <span :class="counter >= 0 ? 'text-success' : 'text-danger'">
      {{ counter }}
    </span>
    <br />
    <span :class="classCounter">
      {{ counter }}
    </span>
  </div>
  <br />
  <hr />
  <br />
  <button class="btn btn-sm btn-success" @click="changeCounter(1)">
    Incrementar
  </button>
  <br />
  <hr />
  <br />
  <button class="btn btn-sm btn-success" @click="changeCounter(2)">
    Disminuir
  </button>
  <br />
  <hr />
  <br />
  <button class="btn btn-sm btn-success" @click="changeCounter(3)">
    Restear
  </button>
  <br />
  <hr />
  <br />
  <button
    :disabled="validateCounterArray"
    class="btn btn-sm"
    :class="validateCounterArray ? 'btn-secondary' : 'btn-success'"
    @click="addNumber()"
  >
    Agregar a favoritos
  </button>

  <br />
  <hr />
  <br />
  <h2>Numeros Favoritos</h2>
  <br />
  <table class="table table-dark">
    <thead>
      <tr>
        <th>Indice</th>
        <th>Valor</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(number, index) in arrayCounter" :key="index">
        <th scope="row">{{ index }}</th>
        <td>{{ number }}</td>
      </tr>
    </tbody>
  </table>
</template>
  
<style>
h1 {
  color: red;
}
</style>