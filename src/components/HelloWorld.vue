<template>
  <div>
    {{ msg }}
    <form>
      <button @click="addTodo()">ADD TASK</button>
      <button @click="deleteTodo()">DELETE FINISHED TASKS</button>
      <p>input: <input type="text" v-model="newTodo"></p>
      <p>task: {{ newTodo}}</p>
    </form>
    <ol>
      <div class="task-list">
        <label class="task-list_item" v-for="todo in todos">
          <input type="checkbox" v-model="todo.done"/>
          <template v-if="todo.editing"><button :disabled="todo.done" @click="todo.editing = !todo.editing">EDIT END</button></template>
          <template v-else><button :disabled="todo.done" @click="todo.editing = !todo.editing">EDIT START</button></template>
          <template v-if="todo.done"><s>{{ todo.text }}</s></template>
          <template v-else-if="todo.editing"><input type="text" v-model="todo.text"/></template>
          <template v-else>{{ todo.text }}</template>
          <br>
        </label>
      </div>
    </ol>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      todos:[
        {text:"Learn HTML", done:false, editing:false},
        {text:"Learn CSS", done:false, editing:false},
        {text:"Learn Javascript", done:false, editing:false},
        {text:"Learn PHP", done:true, editing:false}
      ],
      newTodo:""
    }
  },
  methods:{
    addTodo: function(event){
      const text = this.newTodo && this.newTodo.trim();
      if (!text){
        return;
      }
      this.todos.push({
        text:text,
        done:false
      });
      this.newTodo = '';
    },
    deleteTodo: function(event){
      this.todos = this.todos.filter(todo => {
        return todo.done === false;
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
task-list{
  list-style-type: disc;
}
</style>