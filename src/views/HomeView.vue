<template>
  <h1 class="text-center">Vue-3 ToDo App</h1>
  <div class="container mt-5">
    <div class="row">
      <div class="col">
        <form class="d-flex" @submit.prevent="addNewTodo">
          <div class="col-8">
            <div class="mb-3">
              <label for="" class="form-label">New Todo</label>
              <input
                type="text"
                name="todo"
                id="newTodo"
                class="form-control"
                placeholder="Add new Todo"
                aria-describedby="helpId"
                v-model = "newTod"
              />
            </div>
          </div>
          <div class="col-4 text-center">
            <button type="submit" class="btn btn-primary mt-4">Add New Todo </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
  import {ref} from 'vue'
export default {
setup() {
  const newTod = ref('');
  function addNewTodo() {
    console.log(newTod.value)
  }

  return {
    newTod,
    addNewTodo,
  }

}

};
</script>

<style lang="scss" scoped></style>
