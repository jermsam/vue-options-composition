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
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  
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
