<template>
  <div>
    <div class="contenedor">
      <div class="bloque1">
        <div class="parte1">
          <input
            type="text"
            placeholder="Ingrese la tarea a realizar"
            v-model="tarea"
          />
          <input type="date" value="fecha_n" v-model="fecha" />
          <input
            type="checkbox"
            class="priorizar"
            name="priorizar"
            v-model="priorizar"
          />
        </div>
      </div>
      <div class="parte2">
        <div class="bt1">
          <button @click="guardar()" id="Guardar">Guardar</button>
        </div>
        <div class="bt2">
          <button @click="ordenar()" id="ordenar">Ordenar</button>
        </div>
      </div>

      <div class="bloque2">
        <table>
          <thead>
            <tr>
              <th>Actividad</th>
              <th>Prioridad</th>
              <th>Fecha</th>
              <th>Opciones</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(item, i) in registros"
              :key="i"
              :style="
                item.priorizar === 'Alta'
                  ? 'background-color: red; color:white'
                  : ''
              "
            >
              <td>{{ item.tarea }}</td>
              <td>{{ item.priorizar }}</td>
              <td>{{ item.fecha }}</td>
              <td>
                <button @click="eliminar(i)">❌</button>
                <button @click="editar(item, i)">📝</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref } from "vue";
let registros = ref([]);
let fecha = ref("");
let priorizar = ref("");
let tarea = ref("");

function guardar() {
  registros.value.push({
    tarea: tarea.value,
    priorizar: priorizar.value ? "Alta" : "Baja",
    fecha: fecha.value,
  });
  ({
    tarea: (tarea.value = ""),
    priorizar: (priorizar.value = ""),
    fecha: (fecha.value = ""),
  });
}
function eliminar(i) {
  registros.value.splice(i, 1);
}
function ordenar() {
  registros.value.sort((a, b) => {
    if (a.priorizar === "Alta" && b.priorizar !== "Alta") {
      return -1;
    } else if (b.priorizar === "Alta" && a.priorizar !== "Alta") {
      return 1;
    } else {
      return 0;
    }
  });
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

.contenedor {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: rgb(245, 203, 241);
}

.bloque1 {
  background-color: rgb(245, 203, 241);
  width: 100%;
  height: auto;
  display: flex;
  flex-direction: column;
  margin: 15px;
}

.bloque1 input[type="text"] {
  padding: 20px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 20px;
  width: 70%;
}

.bloque1 input[type="date"] {
  padding: 20px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 20px;
  width: 30%;
}

table {
  border-collapse: collapse;
  border-spacing: 0;
  margin-top: 2%;
  width: 100%;
  margin-bottom: 25px;
  background-color: #f2c3eb;
  margin: 20px;
}
th,
td {
  padding: 10px;
  text-align: left;
  border: 1px solid #ddd;
  text-align: center;
}
th {
  border: 1px solid rgb(0, 0, 0);
  font-family: Arial, sans-serif;
  font-size: 20px;
  overflow: hidden;
  padding: 5px;
  word-break: normal;
  background-color: #ffffff;
  padding: 20px;
  text-align: center;
}

td {
  border: 1px solid rgb(246, 3, 217);
  font-size: 20px;
}
#Guardar {
  font-size: 25px;
  margin: 2px;
  width: 100%;
  border-radius: 6px;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 5px;
  padding: 10px;
  background: linear-gradient(to right, #f6a3a3, #f46363, #f74444);
  border: 2px solid rgb(255, 255, 255);
  color: white;
}
input[type="checkbox"] {
  width: 25px;
  height: 25px;
  margin: 20px;
}
#ordenar {
  font-size: 25px;
  margin: 2px;
  width: 100%;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 5px;
  padding: 10px;
  background: linear-gradient(to right, #f6a3a3, #f46363, #f74444);
  border: 2px solid rgb(255, 255, 255);
  color: white;
}

.bloque2 {
  display: flex;
  align-items: flex-end;
}

.parte2 {
  display: grid;
  justify-content: center;
}
</style>
