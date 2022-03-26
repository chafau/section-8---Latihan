<template>
  <div class="app">
    <input v-model="newTodo" @keyup.enter="addTodo" type="text" />
    <div class="div-btn">
      <button @click="addTodo()">Tambahkan</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: "",
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length > 0) {
        this.$emit("on-new-todo", this.newTodo);
      }
      this.newTodo = "";
    },
  },
};
</script>

<style scoped>
.app {
  display: flex;
}

input {
  width: 80%;
  height: 20px;
  font-size: 19px;
}

.div-btn {
  width: 20%;
  height: 26px !important;
  text-align: center;
}

button {
    background: #28A745;
    border-radius: 30px;
    width: 80%;
    height: 100%;
    color: white;
    opacity: 0.8;
    transition: 0.3s;
}

button:hover {
    opacity: 1;
    cursor: pointer;
}
</style>
