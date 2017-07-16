<template>
  <div class="section">
    <ul class="container">
      <li class="field">
        <p class="control has-icons-left">
          <span class="icon is-small is-left">
            <i class="fa  fa-plus"></i>
          </span>
          <input class="input" placeholder="..." @keyup.enter="create" v-model="newTodo">
        </p>
      </li>
      <todo v-bind="todo" v-for="todo in todos" :key="todo.id" @check="check" @destroy="destroy"
            @updateText="updateText"></todo>
    </ul>
  </div>
</template>

<script>
import Todo from './Todo.vue'

const localStorageKey = 'TODO_APP'

export default {
  components: {
    Todo,
  },
  mounted() {
    this.todos = localStorage.getItem(localStorageKey) ? JSON.parse(localStorage.getItem(localStorageKey)) : []
  },
  data() {
    return {
      nextId: 1,
      newTodo: "",
      todos: [],
    }
  },
  methods: {
    check(id) {
      const todo = this.todos.find((x) => x.id === id)
      todo.checked = !todo.checked
      this.save()
    },
    create() {
      this.todos.push({
        id: this.nextId++,
        text: this.newTodo,
        checked: false,
      })
      this.newTodo = ""
      this.save()
    },
    destroy(id) {
      this.todos = this.todos.filter(x => x.id !== id)
      this.save()
    },
    save() {
      localStorage.setItem(localStorageKey, JSON.stringify(this.todos))
    },
    updateText(nexText, id) {
      // TODO
    }
  },
}
</script>
