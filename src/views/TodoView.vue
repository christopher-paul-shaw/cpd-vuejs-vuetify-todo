<template>
 
<div class="pa-6">

    <v-text-field
      v-model="newTaskTitle"
      label="Create Task"
      :rules="rules"
      hide-details="auto"
      outlined
      append-icon="mdi-plus"
      clearable
      @click:append="addTask"
      @keyup.enter="addTask"
     
    ></v-text-field>
    <v-list
      flat
      subheader
    >
      <div 
        v-for="task in tasks"
        :key="task.id"
      >
        <v-list-item
        @click="toggleDone(task.id)"
        :class="{ 'green lighten-5' : task.done }"    
        >
          <template>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title
                 :class="{ 'text-decoration-line-through' : task.done }"
              >
              {{ task.title }}
              </v-list-item-title>
            </v-list-item-content>
               <v-list-item-action>
          <v-btn 
          
            @click.stop="deleteTask(task.id)"
            icon
          >
            <v-icon color="red lighten-1">mdi-trash-can</v-icon>
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
    data: () => ({ 
      newTaskTitle: '',
      tasks: [
        {
          id: 1,
          title: 'Task 1',
          done: false
        },
        {
          id: 2,
          title: 'Task 2',
          done: true
        },
        {
          id: 3,
          title: 'Task 3',
          done: false
        },
        {
          id: 4,
          title: 'Task 4',
          done: false
        },
      ]
    }),
    methods: {
      toggleDone(id) {
        let task = this.tasks.filter( task => task.id === id)[0]
        task.done = !task.done
      },
      addTask() {
        let newTask = {
          id : Date.now(),
          title : this.newTaskTitle,
          done : false
        }
        this.tasks.push(newTask);
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter( task => task.id !== id)
      }
    }
  }
</script>