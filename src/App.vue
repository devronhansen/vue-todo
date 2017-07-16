<template>
  <div>
    <div class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">Todo App</h1>
        </div>
      </div>
    </div>
    <todo-list></todo-list>
  </div>
</template>

<script>
import TodoList from './TodoList.vue'

export default {
  components: {
    TodoList,
  },
}
</script>

<style lang="scss">
#app {
}
</style>
