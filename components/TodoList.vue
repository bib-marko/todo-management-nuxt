<template>
  <div class="list" id="todo-list">
    <template v-for="todo in filteredTodos">
      <div :key="todo.id">
        <TodoItem :todo="todo" />
      </div>
    </template>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import TodoItem from '@/components/TodoItem'

export default {
  name: 'TodoList',
  components: { TodoItem },
  data() {
    return {
      filters: ['todo', 'done', 'all'],
      activeFilter: 'all'
    }
  },
  computed: {
    ...mapGetters('todos', ['todos']),
    filteredTodos() {
      if (this.activeFilter === 'todo')
        return this.todos.filter(todo => !todo.is_done)
      if (this.activeFilter === 'done')
        return this.todos.filter(todo => todo.is_done)
      return this.todos
    },
    allTodosDone() {
      return (
        this.todos.filter(todo => todo.is_done).length === this.todos.length
      )
    }
  }
}
</script>
