<template>
  <div class="container">
    {{  }}
    <h2 class="t1">Ma Todo App</h2>
    <div class="content">
      <input
        v-model="task.name"
        type="text"
        class="i1"
        placeholder="Ajouter une tâche"
      />
      <input
        v-model="task.hours"
        type="number"
        class="i2"
        placeholder="Nombre d'heures"
      />
      <select v-model="task.assigned" class="i3">
        <option value="">--Please choose an option--</option>
        <option value="Theo">Theo</option>
        <option value="Hugo">Hugo</option>
        <option value="Axelle">Axelle</option>
      </select>
      <button @click="submitTask()" class="btn btn-warning">Ajouter</button>
    </div>
    <table class="table table-hover table-light">
      <thead>
        <tr>
          <th scope="col">Tâches</th>
          <th scope="col">Heures</th>
          <th scope="col">Assigné</th>
          <th scope="col">Status</th>
          <th scope="col">#</th>
          <th scope="col">#</th>
          <th scope="col">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.name }}</td>
          <td>{{ task.hours }}</td>
          <td>{{ task.assigned }}</td>
          <td
            @click="next(index)"
            v-title="'Appuyer pour changer'"
            class="status"
          >
            {{ task.status }}
          </td>
          <td v-title="'Appuyer pour éditer'">
            <div @click="editTask(index)" class="text-center b1">
              <button class="fas fa-pen"></button>
            </div>
          </td>
          <td v-title="'Appuyer pour supprimer'">
            <div @click="deleteTask(index)" class="text-center b2">
              <button class="fas fa-trash"></button>
            </div>
          </td>
          <td v-title="'Sélectionner'">
            <input
              @click="check(task.id)"
              v-model="task.checked"
              type="checkbox"
            />
          </td>
        </tr>
      </tbody>
    </table>
    <div class="details">
      <span class="i8">Il y a actuellement : </span>
      <span class="i9">{{ tasks.length }} tâches</span>
      <button @click="deleteTodos" class="btn btn-warning">
        Supprimer les tâches sélectionnées
      </button>
    </div>
  </div>
</template>

<script>
import "tailwindcss/tailwind.css";
import { v4 as uuidv4 } from "uuid";
export default {
  name: "TodoApp",
  props: {
    msg: String,
  },
  components: {},
  data() {
    return {
      task: {
        id: null,
        name: null,
        hours: null,
        assigned: "",
        status: "to-do",
      },
      editedTask: null,
      set: new Set([]),
      stats: {
        toDo: "to-do",
        inProgress: "in-progress",
        finished: "finished",
      },
      tasks: [
        {
          id: 1,
          name: "Hugo doit manger un gros Kebab.",
          hours: "2",
          assigned: "Hugo",
          status: "finished",
        },
        {
          id: 2,
          name: "Théo doit passer lv5 sur Faceit.",
          hours: "500",
          assigned: "Théo",
          status: "in-progress",
        },
      ],
    };
  },
  methods: {
    submitTask() {
      if (!this.task.name || !this.task.hours || !this.task.assigned)
        return window.alert("Veuillez remplir tous les champs");
      if (this.tasks.assigned) {
        console.log('ok');
      }
      if (this.tasks.assigned) {
        console.log('ah');
      }
      if (this.editedTask === null) {
        this.task.id = uuidv4();
        console.log(this.task.id);
        this.tasks.unshift(this.task);
      } else {
        this.tasks[this.editedTask].name = this.task.name;
        this.tasks[this.editedTask].hours = this.task.hours;
        this.tasks[this.editedTask].assigned = this.task.assigned;
        this.editedTask = null;
      }
      this.task = {
        id: null,
        name: null,
        hours: null,
        assigned: null,
        status: "to-do",
      };
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task.name = this.tasks[index].name;
      this.task.hours = this.tasks[index].hours;
      this.task.assigned = this.tasks[index].assigned;
      this.editedTask = index;
    },
    check(id) {
      if (this.set.has(id)) {
        this.set.delete(id);
      } else {
        this.set.add(id);
      }
    },
    deleteTodos() {
      this.tasks = this.tasks.filter((task) => (task = !this.set.has(task.id)));
    },
    next(index) {
      if (this.tasks[index].status === this.stats.toDo) {
        this.tasks[index].status = this.stats.inProgress;
      } else if (this.tasks[index].status === this.stats.inProgress) {
        this.tasks[index].status = this.stats.finished;
      } else if (this.tasks[index].status === this.stats.finished) {
        this.tasks[index].status = this.stats.toDo;
      }
    },
  },
};
</script>

<style scoped>
table {
  margin-top: 2rem;
}
td {
  border: 1px solid #333;
}
.b1,
.b2,
.status {
  cursor: pointer;
}
thead,
tfoot {
  background-color: #333;
  color: #000;
  border: 1px solid black;
}
thead tr th{
  border: 1px solid black;
}
.show {
  display: flex;
}
.details {
  display: flex;
  display: inline-grid;
}
.container {
  text-align: center;
}
.t1 {
  margin-top: 2rem;
  font-size: 4rem;
}
.content {
  display: flex;
  margin-top: 2rem;
}
.i1,
.i2,
.i3,
.i4 {
  font: 1rem "Fira Sans", sans-serif;
  height: 2rem;
  width: 20rem;
  border-width: 2px;
  text-align: center;
}
.i8 {
  height: 2rem;
  font-size: 2rem;
  padding-bottom: 3rem;
  width: 20rem;
}
.i9 {
  height: 2rem;
  font-size: 2rem;
  padding-bottom: 3rem;
  width: 20rem;
  margin-bottom: 1rem;
}
.i10 {
  height: 2rem;
  width: 20rem;
  border-width: 2px;
}
.content{
  place-content: center;
  align-items: center;
}
.content input{
  border: none;
  border-bottom: 1px solid black;
  max-width: 10%;
  margin-right: 15px;
}
select{
  border: none;
  margin-right: 15px;
}
</style>
