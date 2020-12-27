<template>
  <div class="home pa-1">
    <h1>Todo page</h1>
    <v-list two-line flat>
      <v-text-field
        class="pa-3"
        @click:append="addTask"
        @keyup.enter="addTask"
        v-model="newTaskTitle"
        outlined
        label="Add Task"
        append-icon="mdi-plus"
        hide-
        clearable
      ></v-text-field>
      <v-list-item-group v-model="settings" multiple>
        <div v-for="(value, key) in task" :key="key">
          <v-list-item
            @click="doneTask(value.id)"
            :class="{ 'blue lighten-5': value.done }"
          >
            <template v-slot:default>
              <v-list-item-action>
                <v-checkbox
                  :input-value="value.done"
                  color="primary"
                ></v-checkbox>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title
                  :class="{ 'text-decoration-line-through': value.done }"
                  >{{ value.title }}</v-list-item-title
                >
              </v-list-item-content>
              <v-list-item-action>
                <v-btn icon @click.stop="deleteTask(value.id)">
                  <v-icon color="primary lighten-1">mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </template>
          </v-list-item>
          <v-divider></v-divider>
        </div>
      </v-list-item-group>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Home",
  data: () => ({
    settings: [],
    newTaskTitle: '',
    task: [
      {
        id: 1,
        title: "Wake up",
        done: false,
      },
      {
        id: 2,
        title: "Get bananas",
        done: false,
      },
      {
        id: 3,
        title: "Eat bananas",
        done: false,
      },
    ],
  }),
  methods: {
    doneTask(id) {
      let task = this.task.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.task = this.task.filter((task) => task.id !== id);
    },
    addTask() {
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false
      }
      this.task.push(newTask)
      this.newTaskTitle = ''
    }
  },
};
</script>
