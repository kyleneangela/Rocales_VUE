<template>
  <v-app>
    <v-container>
      <v-card class="pa-5">
        <v-card-title>Task Management</v-card-title>
        <v-card-text>
          <!-- Task Input Form -->
          <v-row>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="newTask.title"
                label="Task"
                placeholder="Enter your task"
                outlined
              ></v-text-field>
            </v-col>

            <v-col cols="12" md="6">
              <v-select
                v-model="newTask.category"
                :items="categories"
                label="Category"
                placeholder="Select a category"
                outlined
              ></v-select>
            </v-col>

            <v-col cols="12">
              <v-btn @click="addTask" color="primary">Add Task</v-btn>
            </v-col>
          </v-row>

          <!-- Task List -->
          <v-list two-line>
            <v-list-item-group>
              <v-list-item v-for="(task, index) in tasks" :key="index">
                <div class="d-flex justify-space-between align-center" style="width: 100%;">
                  <v-list-item-content>
                    <v-list-item-title>{{ task.title }}</v-list-item-title>
                    <v-list-item-subtitle>
                      Created on: {{ formatDate(task.created) }}
                    </v-list-item-subtitle>
                    <v-list-item-subtitle>
                      Category: {{ task.category }}
                    </v-list-item-subtitle>
                  </v-list-item-content>
                  
                  <v-list-item-action>
                    <v-btn icon @click="removeTask(index)">
                      <v-icon>mdi-delete</v-icon>
                    </v-btn>
                  </v-list-item-action>
                </div>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-card-text>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      newTask: {
        title: '',
        category: '',
        created: '',
      },
      tasks: [],
      categories: ['Important', 'Urgent', 'Important and Urgent'],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.title && this.newTask.category) {
        const task = {
          ...this.newTask,
          created: new Date(),
        };
        this.tasks.push(task);
        this.newTask.title = '';
        this.newTask.category = '';
      } else {
        alert('Please enter both task and category');
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    formatDate(value) {
      if (!value) return '';
      const options = { year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' };
      return new Intl.DateTimeFormat('en-US', options).format(value);
    },
  },
};
</script>

<style scoped>
.v-card {
  max-width: 600px;
  margin: auto;
}
</style>
