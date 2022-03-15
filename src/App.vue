<script>
export default {
  data() {
    return {
      isEditing: false,
      ToDo: "",
      ToDos: [],
      selectedTodo: null,
    };
  },
  methods: {
    submitTodo() {
      this.ToDos.push(this.ToDo);
      this.ToDo = "";
    },
    removeTodo(index) {
      console.log(index);
      this.ToDos.splice(index, 1);
    },
    updateTodo() {
      this.ToDos.splice(this.selectedIndex, 1, this.ToDo);
      this.ToDo = "";
      this.isEditing = false;
    },
    editTodo(index, ToDo) {
      this.isEditing = true;
      this.ToDo = ToDo;
      this.selectedIndex = index;
    },
  },
};
</script>

<template>
  <div class="container mt-5">
    <h1 class="display-2 d-flex justify-content-center">ToDo List</h1>
    <div class="row">
      <div class="col-5 m-auto">
        <div v-if="!isEditing" >
          <input
            type="text"
            class="form-control mt-2 mb-2"
            v-model="ToDo"
            placeholder="Masukkan ToDo"
            id="inputTodo"
          />

          <button class="btn btn-primary btn-block" type="submit" value="add" @click="submitTodo">
            simpan
          </button>
        </div>
        <div v-else>
          <input type="text" class="form-control mt-2 mb-2" v-model="ToDo"/>
          <button class="btn btn-primary btn-block" type="submit" value="update" @click="updateTodo">
            Update
          </button>
        </div>

        <ol>
          <li v-for="(ToDo, index) in ToDos" class="mb-2">
            {{ ToDo }}
            <button class="btn btn-secondary mr-1 btn-space" @click="editTodo(index, ToDo)">
              Edit
            </button>
            <button class="btn btn-danger" @click="removeTodo(index)">
              Delete
              </button>
          </li>
        </ol>

      </div>
    </div>
  </div>
</template>

<style>
.btn-space {
  margin-right: 10px;
}
</style>
