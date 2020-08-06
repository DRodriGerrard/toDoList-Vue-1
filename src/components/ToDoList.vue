<template>
  <div class="todolist">
    <h1>toDoList Vue</h1>
    <div class="jumbotron">
      <div class="row">
        <div class="col-sm">
          <form class="form-group">
            <input
              type="text"
              class="form-control"
              placeholder="New Task"
              v-model="tasktitle"
            />
          </form>
        </div>
        <div class="col-">
          <button type="button" class="btn btn-primary" @click="addTask">
            <font-awesome-icon icon="plus" />
          </button>
        </div>
      </div>
    </div>
    <div class="jumbotron" v-if="tasks.length > 0">
      <div class="row">
        <div class="col-lg">
          <task
            v-for="task in tasks"
            v-bind:key="task.id"
            :task="task"
            @deleteEmitted="deleteTask($event)"
            @editEmitted="editTask($event)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import { v4 as uuidv4 } from 'uuid';
import axios from 'axios';
import Task from './Task';

export default {
    name:'ToDoList',

    components:{
        Task
    },

    data(){
        return{
            tasktitle:'',
            tasks:[]
        }
    },

    mounted(){
        this.getTasks();
    },

    methods:{

        async getTasks(){
            await axios.get('http://localhost:3000/tasks').then(response => this.tasks = response.data)
        },

        async addTask(){
            const newDate = new Date();
            const finalDate = newDate.getFullYear()+'-'+newDate.getMonth()+'-'+newDate.getDate()+' at '
            + newDate.getHours()+':'+newDate.getMinutes()+':'+newDate.getSeconds();

            const newTask = {
                id: uuidv4(),
                title:this.tasktitle,
                created:finalDate,
                completed:false
            }

            await axios.post('http://localhost:3000/tasks', newTask)
            .then( response => {
                response;
                this.tasktitle = '';
                this.getTasks();
            })
            .catch(err => console.log(err))
        },

        async deleteTask(task){
            await axios.delete('http://localhost:3000/tasks'+'/'+task.id)
            .then( () => this.getTasks())
        },

        async editTask(task){
            await axios.patch('http://localhost:3000/tasks'+'/'+task.id, task)
            .then( () => this.getTasks())
        }
    }
}
</script>