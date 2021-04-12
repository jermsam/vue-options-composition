<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <p># Todos = {{noOfTodos}}</p>
   <p>
     <input 
     style="text-align:center; outline:none; color:green;"
      placeholder="add to do"
      v-model="newTodoName"
      @keyup.enter="addTodo"
      />
    </p>
    <div>
    <ul class="list">
      
      <li class="list-item"  v-for="todo in todos" :key="todo.id">
      <span>item {{todo.name}}</span>
       <button @click="removeTodo(todo.id)">x</button>
      </li>
    </ul>
    
    </div>
    <div class="list">
    <div class="list-item">
    <span>{{data.counter}}</span>
    <button @click="incrementCounter">+</button>
    <button @click="decrementCounter">-</button>
    </div>
    </div>
  </div>
</template>



<script>
// import { defineComponent } from '@vue/composition-api'

import {ref,computed,watch,reactive} from 'vue'

export default {
    name: 'composition',
  setup() {
    let newTodoName = ref('')
    let todos = ref([
        {
          id: 1,
          name: 'one'
        },
         {
          id: 2,
          name: 'two'
        },
         {
          id: 3,
          name: 'three'
        }
      ],)

      
      const addTodo=()=>{
        todos.value.push({
        id:todos.value.length+1,
        name:newTodoName.value
      })
     newTodoName.value=''
      }

    const   removeTodo=(id)=>{
      // alert(this.newTodoName)
     const index=todos.value.findIndex(todo=>todo.id==id)
      // alert(index)
     todos.value.splice(index,1);
    }

    let noOfTodos=computed(()=>(todos.value.length))

const swearWords=['butt hair','willy','fart']

    watch(newTodoName,(newValue)=>{
      if(swearWords.includes(newValue.toLowerCase())){
  newTodoName.value=''
  alert(`stop it!!! you can not say that`)
}
    })

    const data=reactive({
      counter:10
    })

    const incrementCounter =()=>{
      data.counter++;
    }

     const decrementCounter =()=>{
      data.counter--;
    }

    return {
      newTodoName,
      todos,
      addTodo,
      removeTodo,
      noOfTodos,
      data,
      incrementCounter,
      decrementCounter
    }
  },
}



// @ is an alias to /src
 /*
export default {
   
  name: 'Composition',
  components: {
    
  },

  data:()=>({
    newTodoName:'',
      todos:[
        {
          id: 1,
          name: 'one'
        },
         {
          id: 2,
          name: 'two'
        },
         {
          id: 3,
          name: 'three'
        }
      ],
      swearWords:['butt hair','willy','fart']
  }),
  methods:{
    addTodo: function(){
      // alert(this.newTodoName)
      this.todos.push({
        id:this.todos.length+1,
        name:this.newTodoName
      })
      this.newTodoName=''
    },
    removeTodo: function(id){
      // alert(this.newTodoName)
     const index=this.todos.findIndex(todo=>todo.id==id)
      // alert(index)
      this.todos.splice(index,1);
    },
  },
  computed:{
    noOfTodos(){
      return this.todos.length
    }
  },
  watch:{
    newTodoName(newValue){
if(this.swearWords.includes(newValue.toLowerCase())){
  this.newTodoName=''
  alert(`stop it!!! you can not say that`)
}
    }
  }
  
}
*/

</script>


<style scoped>
span{
  font-size:2rem;
  color:green;
  font-weight:bold;
  text-transform: uppercase;
   text-align: right;
}
 button {
  width:5rem;
  padding:1rem;
  margin: 0 10px;
  background-color: green;
  color: #fff;
}
button:hover{
background-color: greenyellow;
color:green
}
button:focus{
background-color: rgb(34, 53, 4);
color:white
}
.list{
display:flex;
  flex-direction: column;
  align-items: center;

}
.list-item{
  margin: 0.5rem;
  display:flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width:20rem;
 
}
</style>
