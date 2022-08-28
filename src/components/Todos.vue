<template>
  <div>
    <h3>Todos</h3>
    <div class="legend">
      <span>Double click to mark as complete</span>
      <span>
        <span class="incomplete-box"></span> = Incomplete
      </span>
      <span>
        <span class="complete-box"></span> = Complete
      </span>
    </div>
    <div class="todos">
      <div
        @dblclick="onDblClick(todo)"
        :key="todo.id"
        v-for="todo in allTodos"
        class="todo"
        v-bind:class="{'is-complete':todo.completed}"
      >
        {{ todo.title }}
        <button v-on:click="deleteTodo(todo.id)">delete</button>
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters, mapActions } from 'vuex';
  export default {
    name:"Todos",
    methods: {
      ...mapActions(["fetchTodos", "deleteTodo", "updateTodo"]),
      onDblClick(todo) {
        const updatedTodo = {
          id: todo.id,
          title: todo.title,
          completed: !todo.completed
        }
        this.updateTodo(updatedTodo);
      }
    },
    computed:mapGetters(["allTodos"]),
    created(){
      this.fetchTodos();
    }
  }
</script>

<style>

</style>