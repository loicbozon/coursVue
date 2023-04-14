<script setup>
import { ref } from 'vue';

const arrayTodo = ref([]);
const arrayDone = ref([]);
const arrayInProgress = ref([]);

const form = ref({
  title: "",
  time: 0,
  users: "",
});

const Todofnct = () => {
  arrayTodo.value.push(form.value);
  form.value = {
    title: "",
    time: 0,
    users: "",
  }
}

const InProgressAFaire = (index) => {
  arrayInProgress.value.push(arrayTodo.slice(index, 1)[0])
}

const SupprAFaire = (index) => {
  arrayInProgress.value.splice(index, 1)
}
</script>



<template>
  <div class="about">
    <h1>Ma bite au bord de l'eau ca fait un radeau</h1>

    <div>
      <input type="text" name="title" v-model="form.title">
      <input type="text" name="time" v-model="form.time">
      <select name="users" v-model="form.users">
        <option value="option1">Option 1</option>
        <option value="option2">Option 2</option>
        <option value="option3">Option 3</option>
      </select>

      <button @click="Todofnct">Ajoutez une tache</button>
    </div>

    <div v-for="element in arrayTodo">
      {{ element.title }}
      {{ element.time }}
      {{ element.users }}

      <button @click="InProgressAFaire(index)"> En cours</button>
      <button @click="SupprAFaire(index)"> Supprimer</button>
    </div>


  </div>
</template>
  
<!-- <style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
   -->