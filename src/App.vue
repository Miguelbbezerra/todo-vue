<template>
  <!-- Content -->
  <div class="px-3 py-10 md:px-10">
    <div class="w-full sm:w-1/2 lg:w-1/3 mx-auto">
      <!-- Todo spinner -->
      <SpinnerTodo v-if="loading" />
      <!--/ Todo spinner -->

      <template v-else>
        <!-- Todo form -->
        <TodoFormAdd />
        <!--/ Todo form -->

        <!-- Todo items -->
        <TodoItems v-if="$store.state.todos.length"/>
        <!--/ Todo items -->

        <!-- Todo empty -->
        <TodoEmpty v-else/>
        <!--/ Todo empty -->
      </template>
    </div>
  </div>
  <!--/ Content -->
</template>

<script>
import SpinnerTodo from "./components/SpinnerTodo.vue";
import TodoFormAdd from "./components/TodoFormAdd.vue";
import TodoItems from "./components/TodoItems.vue";
import TodoEmpty from "./components/TodoEmpty.vue";

export default {
  name: "App",
  components: {
    SpinnerTodo,
    TodoFormAdd,
    TodoItems,
    TodoEmpty,
  },
  data() {
    return {
      loading: false,
    };
  },
  created() {
    this.loading = true
    this.$store.dispatch('getTodos').finally(() => {
      this.loading = false
    })
  }
};
</script>