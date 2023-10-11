<template>
  <TodoActions>
    <template slot-scope="{ load, todoActions }">
      <ul :class="`choice-list todo-item ${taskStatus && 'done'}`">
        <li class="choice-list__item task-card-item">
          <input
            :id="`checkbox-${todo.id}`"
            type="checkbox"
            class="checkbox"
            @click="checkTask(taskStatus)"
          />
          <label :for="`checkbox-${todo.id}`" class="todo-content">
            <!-- <input type="text" v-model="todo.title" /> -->
            <div class="task-content">
              <span>{{ todo.title }}</span>
            </div>
          </label>
          <span class="choice-list__aside">
            <button
              class="btn task-action-star"
              @click="load(todoActions.delete, todo)"
            >
              <i class="fa fa-star" aria-hidden="true"></i>
            </button>
            <button
              class="btn task-action-trash"
              @click="load(todoActions.delete, todo)"
            >
              <i class="fa fa-trash" aria-hidden="true"></i>
            </button>
          </span>
        </li>
      </ul>
    </template>
  </TodoActions>
</template>

<script>
import TodoActions from '@/components/TodoActions'

export default {
  name: 'TodoItem',
  components: {
    TodoActions
  },
  props: {
    todo: { type: Object, required: true }
  },
  data() {
    return {
      taskStatus: false
    }
  },
  methods: {
    routeTo(id) {
      this.$router.push(`todos/${id}`)
    },
    checkTask(value) {
      return (this.taskStatus = value ? false : true)
    }
  }
}
</script>

<style scoped>
.todo-content {
  width: 90%;
}
.todo-item.done .todo-content span {
  text-decoration: line-through;
  color: HSL(var(--color-purple)) !important;
}
.task-content {
  margin-left: 2.5em;
  margin-top: -1.5em;
}

.btn {
  background-color: transparent; /* Blue background */
  border: none; /* Remove borders */
  font-size: 16px; /* Set a font size */
  cursor: pointer; /* Mouse pointer on hover */
  color: #dadada;
}

/* Darker background on mouse-over */
.task-action-trash :hover {
  color: rgb(255, 75, 75);
}

.task-action-star :hover {
  color: rgb(255, 185, 35);
}

.choice-list__aside {
  display: flex;
  justify-content: right;
  align-items: right;
  font-size: 1.4rem;
  width: 10%;
}
</style>
