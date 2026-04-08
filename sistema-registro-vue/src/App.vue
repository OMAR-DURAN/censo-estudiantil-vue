<script setup>
import { ref } from 'vue';

const datosAlumno = ref({
  nombre: '',
  apellido: '',
  sexo: '',
  areaEstudio: ''
});

const registrosGuardados = ref([]);

const procesarRegistro = () => {
  if (datosAlumno.value.nombre && datosAlumno.value.areaEstudio) {
    registrosGuardados.value.push({ ...datosAlumno.value });
    // Limpiar campos
    datosAlumno.value = { nombre: '', apellido: '', sexo: '', areaEstudio: '' };
  }
};
</script>

<template>
  <div class="panel-control">
    <header class="encabezado">
      <h1>Censo de Estudiantes - Unidad V</h1>
      <p>Gestión Reactiva con Vue.js & Vite</p>
    </header>

    <div class="contenedor-principal">
      <form @submit.prevent="procesarRegistro" class="formulario-estilo">
        <div class="campo">
          <label>Nombres:</label>
          <input v-model="datosAlumno.nombre" type="text" placeholder="Escriba aquí..." required />
        </div>

        <div class="campo">
          <label>Apellidos:</label>
          <input v-model="datosAlumno.apellido" type="text" placeholder="Escriba aquí..." required />
        </div>

        <div class="campo">
          <label>Género:</label>
          <div class="opciones-radio">
            <label><input type="radio" v-model="datosAlumno.sexo" value="Masculino" /> Masculino</label>
            <label><input type="radio" v-model="datosAlumno.sexo" value="Femenino" /> Femenino</label>
          </div>
        </div>

        <div class="campo">
          <label>Carrera Universitaria:</label>
          <select v-model="datosAlumno.areaEstudio" required>
            <option disabled value="">-- Seleccione Carrera --</option>
            <option>Ingeniería de Software</option>
            <option>Ciberseguridad</option>
            <option>Redes y Telecomunicaciones</option>
          </select>
        </div>

        <button type="submit" class="boton-guardar">Registrar en Tabla</button>
      </form>

      <table class="tabla-datos">
        <thead>
          <tr>
            <th>Estudiante</th>
            <th>Género</th>
            <th>Carrera</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, i) in registrosGuardados" :key="i">
            <td>{{ item.nombre }} {{ item.apellido }}</td>
            <td>{{ item.sexo }}</td>
            <td>{{ item.areaEstudio }}</td>
          </tr>
          <tr v-if="registrosGuardados.length === 0">
            <td colspan="3" style="text-align: center;">Esperando datos...</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style>
.panel-control { max-width: 900px; margin: auto; padding: 20px; font-family: sans-serif; }
.encabezado { text-align: center; color: #42b883; border-bottom: 2px solid #eee; margin-bottom: 20px; }
.contenedor-principal { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
.formulario-estilo { background: #fdfdfd; padding: 20px; border: 1px solid #ddd; border-radius: 8px; }
.campo { margin-bottom: 15px; }
.campo label { display: block; font-weight: bold; margin-bottom: 5px; }
input[type="text"], select { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.boton-guardar { background: #35495e; color: white; border: none; padding: 10px; width: 100%; cursor: pointer; border-radius: 4px; }
.tabla-datos { width: 100%; border-collapse: collapse; }
.tabla-datos th, .tabla-datos td { border: 1px solid #ddd; padding: 10px; text-align: left; }
.tabla-datos th { background: #42b883; color: white; }
</style>