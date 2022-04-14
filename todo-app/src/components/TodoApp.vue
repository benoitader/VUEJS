<template>
  <div class="container">
    <h2 class="text-center mt-5">Ma Todo List Application</h2>

    <div class="d-flex">
      <input v-model="tache" type="text" placeholder="Ajouter une tâche" class="form-control">
      <button @click="ajoutTache" class="btn btn-warning rounded-0">Entrer</button>
    </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Tâches</th>
          <th scope="col">Responsable de la tâche</th>
          <th scope="col">Estimation de temps</th>
          <th scope="col">Statut</th>
          <th scope="col" class="text-center">Modifier</th>
          <th scope="col" class="text-center">Supprimer</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(tache, index) in taches" :key="index">
          <td>
            <span :class="{'done': tache.statut === 'done'}">{{tache.nom}}</span>
          </td>
          <td>
            Théo
          </td>
          <td style="width: 120px">
            <span class="pointer" @click="changerStatut(index)"
              :class="{'text-danger': tache.statut === 'à faire',
              'text-warning': tache.statut === 'en cours',
              'text-success': tache.statut === 'done'
              }"
            >
              {{ firstCharUpper(tache.statut) }}
            </span>
          </td>
          <td>
            5 heures
          </td>
          <td>
            <div class="text-center" @click="modifierTache(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="supprimerTache(index)">
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
  nom: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return {
      tache: '',
      tacheModifie: null,
      statutsDisponible: ['done', 'en cours', 'à faire'],

      taches: [
        {
          nom: 'Apprendre à faire une Todo List.',
          statut: 'done'
        },
        {
          nom: "Réaliser l'élective VueJS.",
          statut: 'en cours'
        }
      ]
    }
  },

  methods: {
    ajoutTache(){
      if(this.tache.length === 0) return;

      if(this.modifierTache === null){
        this.taches.push({
          nom: this.tache,
          statut: 'done'
        });
      }else{
        this.taches[this.modifierTache].nom = this.tache;
        this.modifierTache = null;
      }

      this.tache = '';
    },

    supprimerTache(index){
      this.taches.splice(index, 1);
    },

    modifierTache(index){
      this.tache = this.taches[index].nom;
      this.modifierTache = index;
    },

    changerStatut(index){
      let newIndex = this.statutsDisponible.indexOf(this.taches[index].statut);
      if(++newIndex > 2) newIndex = 0;
      this.taches[index].statut = this.statutsDisponible[newIndex];
    },

    firstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);
    }
  }
};

</script>

<style scoped>

.pointer{
  cursor: pointer;
}

.done{
  text-decoration: line-through;
}

</style>
