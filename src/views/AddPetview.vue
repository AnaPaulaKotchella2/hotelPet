<script setup>
import { onMounted, ref } from 'vue';
import { RouterLink, useRouter } from 'vue-router';

const novoPet = ref ({
     nome:'',
  especie:'',
  TutorId:'',
})
const Router = useRouter();

const API_URL = "http:/localhost: 3000"

const tutores = ref({});

async function carregarTutores(){
  const resposta = await fetch (`${API_URL}`/tutores);
  console.log('load tutores', tutores);
  tutores.value = await resposta.json();
}

async function salvaPet (){

 await fetch (`${API_URL}/pets`, {

  method: 'POST',
  header: {
 'Content-type': 'application/json',
  },
  body: JSON.stringify(novoPet.value),
 

});
 router.push('/pets');

}

onMounted(carregarTutores);

</script>

<template>

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
 
    <p v-if="carregandoTutores">carregando tutores...</p>
    <div v-else>

      <p
      v-if="erro"
      class="alert alert-danger"
      role="alert"
      ></p>

    </div>

     <form @submit.prevent="salvarPet">

      <div class="col-md-6">


        <label
         for="nome" 
        class="from-label">Nome do pet</label>



        <input 
        type="text"
        id="nome"
        v-model="novoPet.nome"
        class="form-control" 
        required>


      </div>
      <div class="col-md-6">


        <label
         for="nome" 
        class="from-label">Especie</label>

        <select 
        id="especie"
        v-model="novoPet.especie"
        class="form-select"
        required
        
        >
      <option 
      value=""
      disabled>

        Selecionar a Espécie

      </option>
      <option value="Cachorro">Cachorro</option>

      <option value="Gato">Gato</option>

      </select>

      </div>

       <div class="col-md-6">


        <label
         for="nome" 
        class="from-label">Especie</label>

        <select 
        id="tutor"
        v-model="novoPet.tutorid"
        class="form-select"
        required
        
        >
      <option 
      value=""
      disabled>

        Selecionar Tutor

      </option>
      <option v-for="tutor in tutores" 
      :key="tutor.id"
      :value="tutor.id"
      {{ tutor.nome }};
      
      
      >
    
    </option>
      

      </select>

      </div>

    </form>


  </div>
</template> //========================================================//












 <main class="container py-5">
    <div
      class="alert alert-success"
      role="alert"
    >
      <h1 class="alert-heading">
        <i class="bi bi-check-circle-fill me-2"></i>
        Projeto configurado!
      </h1>

      <p class="mb-0">
        Vue.js, Vue Router, Bootstrap e Bootstrap Icons estão funcionando.
      </p>
    </div>
  </main>



  
</template>