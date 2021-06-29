<template>
  <div class="pa-5">
    <v-text-field
      @click:append="addTask"
      @keyup.enter="addTask"
      v-model="newTask"
      label="Adicionar tarefa"
      solo
      append-icon="mdi-plus"
      hide-details
      clearable
    ></v-text-field>

    <v-list
      flat
    >
      <div
        :key="task.id"
        v-for="task in tasks"
      >
          <v-list-item
            @click="doneTask(task.id)"
            :class="{ 'indigo lighten-5': task.done }"
          >
            <template v-slot:default>
              <v-list-item-action>
                <v-checkbox :input-value="task.done"></v-checkbox>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title>{{ task.title }}</v-list-item-title>
              </v-list-item-content>
              <v-list-item-action>
                <v-btn icon>
                  <v-icon color="#e3e3e3" @click="deleteTask(task.id)">mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </template>          
          </v-list-item>

          <v-divider></v-divider>
      </div>
      
    </v-list>

  </div>
</template>

<script>
  export default {
    name: 'Home',
    data() {
      return {
        newTask: '',
        tasks: [
          {
            id: 1,
            title: 'Acordar',
            done: false
          },
          {
            id: 2,
            title: 'Acordar 2',
            done: false
          },
          {
            id: 3,
            title: 'Acordar 3',
            done: false
          },
        ]
      }
    },

    methods: {
      addTask() {
        this.tasks.push({
          id: Date.now(),
          title: this.newTask,
          done: false
        })
        this.newTask = ''
      },
      doneTask(id) {
        let task = this.tasks.filter(task => task.id === id)[0]
        task.done = !task.done
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      }
    }

  }
</script>
