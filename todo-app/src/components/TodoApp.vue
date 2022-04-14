<template>
  <div class="container">
    <h2 class="text-center mt-5">Ma Todo List Application</h2>

    <div class="d-flex">
      <input v-model="tache" type="text" placeholder="Ajouter une tâche" class="form-control">
      <button @click="submitTache" class="btn btn-warning rounded-0">Entrer</button>
    </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Tâches</th>
          <th scope="col">Statut</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(tache, index) in taches" :key="index">
          <th>{{tache.name}}</th>
          <td>{{tache.statut}}</td>
          <td>
            <div class="text-center">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return {
      tache: 'Hello World',
      taches: [
        {
          name: 'Dire à Hugo de fermer sa gueule.',
          statut: 'Fait'
        },
        {
          name: 'Manger le riz curry de Benoit.',
          statut: 'En cours'
        }
      ]
    }
  },

  methods: {
    submitTache(){
      console.log(this.tache)
    }
  }
};

</script>

<style scoped>
</style>
