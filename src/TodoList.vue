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
      <draggable v-model="todos" @update="save">
        <todo v-bind="todo" v-for="todo in todos" :key="todo.id" @check="check" @destroy="destroy"
              @updateText="update"></todo>
      </draggable>
    </ul>
  </div>
</template>

<script>
import Todo from './Todo.vue'
import draggable from 'vuedraggable'

export default {
  components: {
    Todo,
    draggable,
  },
  props: {localStorageKey: String},
  data() {
    let initData = {
      nextId: 1,
      newTodo: "",
      todos: [],
      storageKey: this.localStorageKey || 'TODO_APP'
    }
    if (localStorage.getItem(initData.storageKey)) {
      initData = {...initData, ...JSON.parse(localStorage.getItem(initData.storageKey))}
    }
    return initData
  },
  methods: {
    check(id) {
      const todo = this.todos.find(x => x.id === id)
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
      localStorage.setItem(this.storageKey, JSON.stringify(
        {
          todos: this.todos,
          nextId: this.nextId,
        }
      ))
    },
    update(text, id){
      this.todos.find(x => x.id === id).text = text
    }
  },
}
</script>

<style lang="sass">
  .container
    margin: auto
    @media screen and (min-width: 1384px)
      max-width: 800px
</style>
