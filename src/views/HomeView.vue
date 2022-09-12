<template>
  <h1 class="text-center">Vue-3 ToDo App</h1>
  <div class="containerfluid mt-5 p-5">
    <div class="row">
      <div class="col">
        <form class="d-flex" @submit.prevent="addnewTodoo">
          <div class="col-8">
            <div class="mb-3">
              <input
                type="text"
                name="todo"
                id="newTodoo"
                class="form-control"
                placeholder="Add new Todo"
                aria-describedby="helpId"
                v-model="newTodo"
              />
            </div>
          </div>
          <div class="col-4 text-center">
            <button type="submit" :disabled="newTodo == ''" class="btn btn-primary">
              Add New Todo
            </button>
          </div>
        </form>
      </div>
      <div class="col">
        <div class="todoList">
          <div class="d-grid gap-2 ">
            <div class="row">
              <div class="col text-start">
                <button type="button" :disabled="todos == ''" @click="markAllDone" class="btn btn-primary">
                  Mark All Done
                </button>
              </div>
              <div class="col text-end">
                <button type="button" class="btn btn-danger" :disabled="todos == ''" @click="removeAll">Remove All</button>
              </div>
            </div>
          </div>
          <div class="card mt-3 mb-2 p-3" v-for="(todo, index) in todos" :key="index">
            <div class="row">
              <div class="col-9">
                <h3 :class="{ done: todo.done }" @click="itemDone(todo)">
                  {{ todo.content }}
                </h3>
              </div>
              <div class="col-3">
                <button type="button" class="btn btn-danger" @click="removeTodo(index)">
                  Remove
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);
    function addnewTodoo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }
    function itemDone(event) {
      event.done = !event.done;
    }
    function removeTodo(event) {
      todos.value.splice(event, 1);
    }
    function markAllDone() {
      todos.value.forEach((element) => {
        element.done = true;
      });
    }
    function removeAll() {
      todos.value=[]
    }
    return {
      newTodo,
      todos,
      addnewTodoo,
      itemDone,
      removeTodo,
      markAllDone, removeAll
    };
  },
};
</script>

<style lang="scss">
.todoList {
  h3 {
    cursor: pointer;
  }
  .done {
    text-decoration: line-through;
    color: green !important;
  }
}
</style>
