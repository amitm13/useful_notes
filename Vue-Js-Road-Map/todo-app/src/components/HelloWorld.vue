<template>
  <div class="container">
    <h2 class="font-bold m-3">ToDo App</h2>
    <div>
      <input type="text" class="h-30 p-2 rounded-md mb-2" placeholder="To Do Title" v-model="todo_title"><br/>
      <button class="h-30 p-2 rounded-md mb-2 hover:bg-blue-700 bg-blue-600 text-white shadow w-4/12" v-on:click="addToDoItem">Add</button>
    </div>

    <div class="bg-yellow-300 h-30 w-4/12 mx-auto my-3 rounded-md py-2">
      please add todo item.
    </div>
    <div v-for="(item, index) in todo_list" :key="index" class="bg-white w-4/12 h-auto py-2 mt-2 mx-auto rounded-md shodow-lg">
    <span v-bind:class="(item.done) ? 'line-through' : 'font-bold'">{{ item.name }}</span>
    <img src="https://img.icons8.com/fluency/48/000000/delete-sign.png" class="float-right  w-10 h-10 p-2" v-on:click="removeToDoItem(index)"/>

    <img src="https://img.icons8.com/color/48/000000/checkmark.png" class="float-right  w-10 h-10 p-2" v-on:click="markAsDone(index)" />

    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return {
      todo_title:'',
      todo_list:[]
    }
  },
  methods:{
    addToDoItem(){
      if (this.todo_title=='') {
        alert('Todo title field is required!');
        return;
      }
      this.todo_list.push({name:this.todo_title,done:false});
      this.todo_title = '';
    },
    removeToDoItem(index){
      this.todo_list.splice(index,1);
    },
    markAsDone(index){

      this.todo_list[index].done = (this.todo_list[index].done) ? false : true;
    }
  }
  
}
</script>
