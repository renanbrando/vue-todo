<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="todo" @change="addTodo">
    <h1>My tasks</h1>
    <h4 v-for="(t, index) in todos" :key="index">
      <div>
        <input :value="t.desc" :disabled="t.editable" @change="editTodo($event, t.id)">
        <button @click="deleteTodo(t)">Deletar</button><button @click="t.editable = !t.editable">Editar</button>
      </div>
    </h4>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: {
      type: String,
      default: 'Hello World'
    }
  },
  data(){
    return {
      todo: "",
      todos: []
    }
  },
  methods: {
    addTodo(){
      let data = {
        id: new Date(),
        desc: this.todo,
        editable: true
      }
      this.todos.push(data)
    },
    deleteTodo(todo){
      this.todos.splice(this.todos.findIndex(item => todo.id == item.id), 1)
    },
    editTodo(event, id){
      const index = this.todos.findIndex(item => id == item.id)
      this.todos[index].desc = event.target.value
      // eslint-disable-next-line no-console
      console.log(this.todos)
    }
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
</style>
