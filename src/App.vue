<template>
<h1>Todo project</h1>
<hr>
<AddItem 
@add-task="addTask"/>
<label>Select filter</label>
<select v-model="filter">
                <option value="all">All</option>
                <option value="end">Finished</option>
                <option value="not-end">Not completed</option>
</select>
<TodoList 
  :tasks="filterSelection"
  @remove-task="removeTask"
  @checkbox-changed="changeTodo"
  @name-changed="changeTodo"
  v-if="filterSelection.length!==0"
/>
<img src="./assets/no-items.jpg" v-else/>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddItem from "@/components/AddItem";

export default {
  name: 'App',
  data(){
    return{
        tasks:[],
        filter:'all'
    }
  },
  components: {
    TodoList, AddItem
  }, 
  methods: {
      
      reactStatusArr()
      {
        this.tasks=this.tasks.filter(t=>t);
      },
      removeTask(id)
      {
        this.tasks=this.tasks.filter(t=>t.id!==id);
      },
      addTask(obj)
      {
         this.tasks.push(obj);
         this.reactStatusArr();
      },
      changeTodo(obj){
        const index = this.tasks.findIndex(item=> item.id==obj.id);
        this.tasks[index]=obj;
        this.reactStatusArr();
      }
      
  },
  computed:{
    filterSelection()
      {
        if(this.filter=='all')
        {
          return this.tasks.filter(task => task);
        }
        if(this.filter=='end')
        {
          return this.tasks.filter(task => task.completed == true);
        }
        if(this.filter=='not-end')
        {
          return this.tasks.filter(task => task.completed === false);
        }
        return 0;
      }
  },
  watch:{
    tasks(value)
    {
      localStorage.setItem('todos', JSON.stringify(value));
    }
  },
  mounted(){
    if(!localStorage.todos || JSON.parse(localStorage.todos).length==0)
    {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then(response => response.json())
      .then(json => this.tasks=json)
    }else {
        this.tasks= JSON.parse(localStorage.todos);
    }
      
  }
}
</script>

<style>
body{
  background: linear-gradient(135deg, #f5af19, #f12711);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
select{
  margin: 1rem;
}
</style>
