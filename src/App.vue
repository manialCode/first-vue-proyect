<script setup>
import { ref, computed  } from 'vue';

const hi = 'Soy un Vue dinámico'
//#region 
const style = {
  "height": "6rem",
  "width": "100%",
  "padding": "20px",
  "background": "black",
  "border-radius": "50px",
}
const style2 = {
  "height": "7rem",
  "width": "90%",
  "padding": "20px",
  "background": "#777",
  "border-radius": "10%",
  "border": "10px solid #55f"
}

const color = ["#5eff00", "#695cfe", "#777"]
//#endregion
//#region 
let state = false;
const state2 = ref(true);

const name = "Vue 3";
const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒", 'pussy'];
const arrayFrutasObj = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
  },
];
const arrayFrutasObj2 = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
    stock: 0,
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
    stock: 10,
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
    stock: 20,
  },
];
// method
const btn = ("click", () => {
  (state2.value) ? state2.value = false : state2.value = true;
  console.log(state2);
})
//#endregion

const counter = ref(0);
const increment = () => counter.value++;
const decrement = () => counter.value--;
const reset = () => counter.value = 0;
const classCounter = computed(() => {
    if (counter.value === 0) return "zero";
    return counter.value > 0 ? "positive" : "negative";
});
const resetList = () => numList.value = []

const numList = ref([]);

const add = () => [numList.value.push(counter.value)]
const blockAddButton = computed(() => {
  const jj = numList.value.find(x => x === counter.value)
  return jj || jj === 0
})

</script>

<template>
  <div class="container__h">
    <div class="h1">
      <h1>Buenas noches ... {{ hi.toLocaleUpperCase() }}</h1>
      <div id="numbList">
        <h2 v-for="(number, index) in numList" :key="index"> {{ number }} </h2>
      </div>
    </div>
<section>
  
      <button type="button" @click="increment"> Sumar uno</button>
      <button type="button" @click="decrement"> Restar uno</button>
      <button type="button" @click="reset" @click.middle="resetList"> Reiniciar</button>
      <button type="button" :disabled="blockAddButton" @click="add"> Añadir</button>

      <!-- !-- Hacer que la aplicación detecte la hora y que salude según en que etapa del dia estas --> 
    </section>
    <div class="h2">
      <h2 :class="classCounter"> {{ counter }}
      </h2>   
    </div>

  </div>


  <div v-show="state" class="global">
    <template v-for="item in arrayFrutasObj2" :key="item.name">
      <ul>
        <li v-if="item.stock > 0">
          {{ item.name }} - {{ item.price }}
        </li>
      </ul>
    </template>

    <h2 v-if="state2 === true">Estoy Activo!</h2>
    <h2 v-else="state2 === false">Estoy inactivo!</h2>
    <h2>{{ state2 }}</h2>
    <button type="button" @click="btn"> Presiona para cambiar state</button>

    <ul>
      <li v-for=" (value, property, index) in style" :key="value">
        {{ index + 1 }} - {{ property }}: {{ value }}
      </li>
    </ul>/
    <ul>
      <li v-for=" (fruta, index) in arrayFrutasObj" :key="fruta.name">{{ index + 1 }} - {{ fruta.name }} - {{
    fruta.price
}} - {{ fruta.description }}
      </li>
    </ul>
    <ul v-show="state">
      <li v-for=" (fruta, index) in arrayFrutas" :key="index">{{ index + 1 }} - {{ fruta }}</li>
    </ul>
    <h2 :style="`color: ${color[1]}`">Colores de prueba = {{ color }}</h2>


    <p v-if="state === true" v-bind:style="`${style2}`">
      Estoy activo
    </p>
    <p v-else-if="state === false">
      Estoy inactivo
    </p>
    <p v-else>
      Soy de genero no binario
    </p>

    <h2 v-show="state">Estoy activo con v-show</h2>
  </div>

</template>

<style>
body {
  top: 0;
  left: 0;
}
body {
  background-color:#f5f5f5;
  box-sizing: border-box;
  scroll-behavior: smooth;
}

.h2 .positive{
  color:green;
}
.h2 .negative{
  color: red;
}
.h2 .zero{
  color: white;
}

.h1 {
  height: 6rem;
  width: 100%;
  background: black;
  border-radius: 30px;
  box-shadow: 0 .1rem .4rem rgba(0, 0, 0, .3);
}

.container__h #numList{
  height: 6rem;
  width: 100%;
  background-color: red;
  z-index: 10;
  
}

#numbList{
  display: flex;
  justify-content: center;
  top:-20px;
  gap: 10px;
}

.container__h #numbList h2{
  font-size: 1.2rem;
  font-weight: 500;
}

/* .container__h {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
} */

.container__h h1 {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  font-weight: 600;
  font-size: 16px;
  text-align: center;
  color: aquamarine;
  padding: 20px;
}

.container__h h2 {
  
  font-size: 1.5rem;
  font-weight: 800;
  font-style: italic;
  color: aqua;
  line-height: 35px;
  text-align: center;
}

.container__h .h2 {
  width: 40px;
  height: 40px;
  box-shadow: 0 .1rem .4rem rgba(0, 0, 0, .3);;
  background-color: #000;
  border-radius: 50px;
  margin: auto;
}

section {
  width: 100%;
  display: grid;
  padding: 10px;
}

button {
  margin: 0 5px;
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6em 1.2em;
  font-size: 10px;
  font-weight: 500;
  font-family: inherit;
  background-color: #f0f0f0;
  cursor: pointer;
  box-shadow: 0 .1rem .4rem rgba(0, 0, 0, .3);;
  transition: border-color 0.25s;
}

button:hover {
  border-color: #646cff;
}

@media (min-width: 320px){
  .h1{
    height: 8rem;
  }
  
  .container__h h1 {
    font-size: larger;
  }

  section{
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
  }

  button{
    width: 100px;
    height: 3rem;
    margin: 10px auto;
  }

  .h2 {
    line-height: 150px;
  }

}



@media (min-width: 428px){
  section {
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 1fr;
  }
} 

@media (min-width: 1024px) {
  
  .container__h h1{
    top: -10px;
  }

  section{
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 1fr;
  }
  .container__h .h2 {
    width: 8rem;
    height: 50px;
    margin: auto;
    }

    .container__h h2{
      font-size: 1.2rem;
      font-weight: 900;
      text-align: center;
      top: 5px;
    }

  button {
    width: 250px;
    height: 3rem;
    padding: 0.6em 1.2em;
    font-size: 13.5px;
    font-weight: 500;
  }

  .container__h {
    height: 7rem;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    gap: 10px;
  }

}
</style>