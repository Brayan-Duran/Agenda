
<template>
  <div>
    <h1>Programa tus actividades</h1>

    <div class="aj">
      <div class="top">
        <h3 style="margin: 0; font-size:50px;">Agendar</h3>
        <input type="text" id="actividad" v-model="actividad" placeholder="ingrese una actividad">
        <input type="date" id="fecha" v-model="fecha">

        <button @click="enviar()" id="agregar">Agregar</button>
        <span style="font-size: 20px; font-weight: 700;">Active para cambiar la prioridad</span> <input type="checkbox" id="cheked" v-model="cheked">
        <button @click="organizar()" id="ordenar">Ordenar</button>
      </div>
    </div>

    <div class="rigth">
      <table>
        <thead>
          <tr>
            <th>Actividad</th>
            <th>prioridad</th>
            <th>Fecha</th>
            <th>Eliminar</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, i) in arr" :key="i">
            <td>{{ item.actividad }}</td>
            <td :style="item.prioridad=== 'alta'? 'background: orange':'' ">{{ item.prioridad }}</td>
            <td>{{ item.fecha }}</td>
            <td >
              <button @click="eliminar(i)">❌</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>


  </div>
</template>

<script setup>

import { ref } from "vue"

let arr = ref([])
let actividad = ref("")
let prio = ref("")
let fecha = ref("")
let cheked = ref("")



function enviar() {

  if (cheked.value) {
    prio.value = "alta"
  } else {
    prio.value = "baja"
  }

  console.log(prio.value)

  const agenda = {
    actividad: actividad.value,
    prioridad: prio.value,
    fecha: fecha.value
  }
  arr.value.push(agenda)
  console.log(arr)
}

function eliminar(i){
  arr.value.splice(i,1) 
}

function organizar() {
  arr.value.sort(function (a, b) {

    return (a.prioridad === 'alta') ? -1 : 1;
  })
}



</script>

<style>
#app {
  width: 100vw;
}

h1 {
  position: relative;
  top: -100px;
  text-align: center;
  margin: 0;
  color:#EC1C5E;
  text-shadow: 5px 5px 8px #c0bfbf;
  display: block;
}

.aj{
  display: grid;
  align-items: center;
  justify-content: center;
  position: relative;
  top: -50px;
  overflow: auto;
}

.top {
  display: flex;
  flex-direction: column;
  background: #f2bc8ca9;
  width: 500px;
  border-radius: 10px;
  display: grid;
  justify-items: center;
  margin-bottom: 20px;
  padding: 20px;
  color: #D8154F;
}

#agregar {
  width: 70px;
  font-size: smaller;
  padding: 10px;
  color: #D8154F;

}

#ordenar {
  width: 70px;
  font-size: smaller;
  padding: 10px;
  color: #D8154F;

}

#actividad{
  width: 300px;
  color: #D8154F;

}

#fecha{
  width: 200px;
  margin: 5px;
  color: #D8154F;

}

.rigth {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

table {
  background: black;
  width: 400px;
}

thead {
  background: cornflowerblue;
}

tbody {
  background: white;
  color: black;
}

body {
  background-image: url(./assets/acti.jpg); 
  background-repeat: no-repeat, repeat;
  background-position: center;
  background-size: cover;
}
</style>
