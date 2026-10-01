<script setup>

import { onMounted, ref} from 'vue';
import { RouterLink } from 'vue-router';

const API_URL = 'http://localhost:3000'

const pets = ref([]);
const tutores = ref([]);
const loading = ref(true);

async function carregarDados() {

  const dadosPets = await fetch(`${API_URL}/pets`);
  pets.value = await dadosPets.json();
  console.log('pets', pets.value)

  const respostaTutores = await fetch ('${API_URL}/tutores')
  tutores.value = await respostaTutores.json();
  console.log('tutores', tutores.value)
  loading.value = false
  
}

function nomeTutor (TutorId){
  for (const tutor of tutores.value) {
    //tutor.id = TutorId
    if( tutor.id == tutorId){
      return tutor.nome;
    }
  }
  return 'Tutor Não encontrado!';
}
onMounted(carregarDados);
</script>

<template>
 <div>
    <header class="mb-4">
      <h1 class="text-2xl font-bold">Listagem de Pets</h1>
      <p class="text-body-secondary mb-0">Cadastro de Pets no sistema.</p>
    </header>

    <RouterLink
      class="btn btn-primary"
      :to="{ name: 'addPet' }"
    >
      Adicionar Pet
    </RouterLink>

    <table>
      <thead>
        <tr>
          <th>Nome</th>
          <th>Idade</th>
          <th>Especie</th>
          <th>Tutor</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="pet in pets" :key="pet.id">
          <td>{{ pet.id }}</td>
          <td>{{ pet.Nome }}</td>
          <td>{{ pet.Idade }}</td>
          <td>{{ pet.Especie }}</td>
          <td>{{ nomeTutor (pet.Tutor) }}</td>
        </tr>
      </tbody>
    </table>

  </div>
</template>
