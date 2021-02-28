<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div class="home">
        <v-text-field
          v-model="newTaskTitle"
          @click:append="addTask"
          @keyup.enter="addTask"
          class="pa-5"
          outlined
          label="Ajouter une tâche"
          append-icon="mdi-plus-box"
          color="success"
          hide-details
          clearable
        ></v-text-field>

        <v-list
          flat
        >
          <div
            v-for="task in tasks"
            :key="task.id"
          >
            <v-list-item

              :class="{'green lighten-5': task.done}"
            >
              <template v-slot:default>
                <v-list-item-action>
                  <v-checkbox
                    @click="doneTask(task.id)"
                    :input-value="task.done"
                    color="success"
                  ></v-checkbox>
                </v-list-item-action>

                <v-list-item-content>
                  <v-text-field
                    v-model="task.title"
                    id="edit"
                    class="d-none"
                  >
                  </v-text-field>

                  <v-list-item-title
                    :class="{ 'text-decoration-line-through' : task.done }"
                  >
                    {{ task.title }}
                  </v-list-item-title>
                </v-list-item-content>

                <v-list-item-action>
                  <v-btn
                    @click.stop="editTask(task.id)"
                    icon>
                    <v-icon color="blue darken-1">mdi-pencil</v-icon>
                  </v-btn>
                  <v-btn
                    @click.stop="deleteTask(task.id)"
                    icon>
                    <v-icon color="red darken-1">mdi-close-box</v-icon>
                  </v-btn>
                </v-list-item-action>
              </template>



            </v-list-item>
            <v-divider></v-divider>
          </div>




        </v-list>
      </div>
    </v-col>
  </v-row>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'


export default {
  name: 'Home',
  data(){
    return{
      newTaskTitle: '',
      updateTask: '',

      tasks: [
        // {
        //   id: 1,
        //   title: 'Wake up',
        //   done: false
        // },
        // {
        //   id: 2,
        //   title: 'learn Vue',
        //   done: false
        // }
      ]
    }
  },
  methods: {
    addTask(){
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false
      }
      this.tasks.push(newTask)
      this.newTaskTitle = ''
    },
    doneTask(id){
      let task = this.tasks.filter(task => task.id === id)[0]
      task.done = !task.done
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id)
    },
    editTask(id){
      console.log(editTask, id)
    }

  }

}
</script>

