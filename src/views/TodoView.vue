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
  arrayInProgress.value.push(arrayTodo.value.slice(index, 1)[0])
}

const DoneAFaire = (index) => {
  arrayDone.value.push(arrayInProgress.value.slice(index, 1)[0])
}

const SupprAFaire = (index) => {
  arrayTodo.value.splice(index, 1)
}

const SupprInProgress = (index) => {
  arrayInProgress.value.splice(index, 1)
}

const EditTask = (index) => {
  this.task = this.tasks[index].name,
    this.editTask = index
}
</script>



<template>
  <div class="about">
    <h1>Ma todo App</h1>

    <div>
      <input type="text" name="title" placeholder="Entrez le nom de votre tache" v-model="form.title">
      <input type="text" name="time" v-model="form.time">
      <select name="users" v-model="form.users">
        <option value="option1">Option 1</option>
        <option value="option2">Option 2</option>
        <option value="option3">Option 3</option>
      </select>

      <button @click="Todofnct">Ajoutez une tache</button>
    </div>

    <div v-if="arrayTodo.length > 0">
      <h1>A faire</h1>
      <div v-for="(element, index) in arrayTodo">
        {{ element.title }}
        {{ element.time }}
        {{ element.users }}

        <button @click="InProgressAFaire(index)"> En cours</button>
        <!-- <button @click="EditTask = true, EditTask(index)"> Editer</button> -->
        <button @click="SupprAFaire(index)"> Supprimer</button>
      </div>
    </div>



    <div v-if="arrayTodo.length > 0">
      <h1>En cours</h1>
      <div v-for="(element, index) in arrayInProgress">
        {{ element.title }}
        {{ element.time }}
        {{ element.users }}

        <button @click="DoneAFaire(index)"> Terminé</button>
        <button @click="SupprInProgress(index)"> Supprimer</button>
      </div>
    </div>

    <div v-if="arrayTodo.length > 0">
      <h1>Terminé</h1>
      <div v-for="(element, index) in arrayDone">
        {{ element.title }}
        {{ element.time }}
        {{ element.users }}
      </div>
    </div>

    <br><br><br><br><br>

    <div>
      Il y a actuellement: <br>
      {{ arrayTodo.length }} taches <br>
      {{ arrayInProgress.length }} taches en cours <br>
      {{ arrayDone.length }} taches effectuées
    </div>

  </div>
</template>

