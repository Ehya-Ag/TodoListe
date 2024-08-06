
<template>
    <h1>Todo liste</h1>
    <form @submit.prevent="addNewTodo">
      <label>New todo</label>
      <input v-model="newTodo" name="newTodo">
      <button>Add new todo</button>
    </form>
    <div>
      <button @click="markAllDone">Mark All Done</button>
      <button @click="removeAll">Remove All</button>
    </div>
    <ul>
    <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
        {{todo.content}}</h3>
      <button @click="removeTodo(index)">Remove Todo</button>

    </li>
    </ul>

</template>



<script>
import { ref, reactive } from 'vue'

export default{
  setup() {
    const newTodo = ref('')
    const todos= ref([]);
    function addNewTodo(){
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
      console.log(newTodo.value)
    }
    function toggleDone(todo){
      todo.done = !todo.done;
    }
    function removeTodo(index){
      todos.value.splice(index, 1)
    }
    function markAllDone(){
      todos.value.forEach((todo) => todo.done = true)
    }
    function removeAll(){
      todos.value = [];
    }
    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAll
    }
  }
}
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
  .done{
    text-decoration: line-through;
  }
  .todo{
    cursor: pointer;
  }
}
</style>
