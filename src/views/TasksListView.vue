<template>
  <v-main class="overflow-hidden mt-2">
    <v-container>
      <v-row>
        <v-col class="pa-1" cols="12" v-for="task in tasks" :key="task.id">
          <v-card>
            <v-card-text>
              <p class="ma-0 pa-0 text-h5 text--primary">{{ task.title }}</p>
              <p class="ma-0 pa-0 text-h5 text--primary">{{ task.project }}</p>
              <p class="ma-0 pa-0 text-h5 text--primary">{{ task.dueTo }}</p>
            </v-card-text>
            <v-card-actions>
              <v-list-item class="grow">
                <v-row align="center" justify="end">
                  <v-btn x-small icon color="grey" @click="editarTasks(task)"
                    ><v-icon>fas fa-pen fa-xs</v-icon></v-btn
                  >
                  <v-btn x-small icon color="grey" @click="deletarTasks(task)"
                    ><v-icon>far fa-trash-alt fa-xs</v-icon></v-btn
                  >
                </v-row>
              </v-list-item>
            </v-card-actions>
          </v-card>
        </v-col>
        <p>
          <v-btn x-large rounded class="orange" :to="{ name: 'newTask' }">
            +
          </v-btn>
        </p>
      </v-row>
    </v-container>
  </v-main>
</template>

<script>
import TasksApi from '@/tasksapi'

export default {
  data: () => {
    return {
      tasks: [],
    }
  },
  methods: {
    listarTarefas() {
      TasksApi.getTasks((data) => {
        this.tasks = data
      })
    },
    deletarTasks(task) {
      TasksApi.deleteTasks(task.id).then(() => {
        this.listarTarefas()
      })
    },
    editarTasks(task) {
      this.$router.push({
        name: 'editTask',
        params: { id: task.id, task: task },
      })
    },
  },
  created() {
    this.listarTarefas()
  },
}
</script>
