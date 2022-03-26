<template>
  <li class="flex">
    <div class="descriptionBeforeEdit" v-if="!isEditing">
      {{ description }}
    </div>

    <form v-else class="formEdit" @submit.prevent="finishEditing()">
      <input
        type="text"
        class="form-control"
        v-model="newTodoDescription"
        ref="newTodo"
      />
    </form>

    <div class="editBtnWrap">
      <button class="editBtn" @click="startEditing()">Edit</button>
    </div>

    <div class="deleteBtnWrap">
      <button class="deleteBtn" @click="$emit('on-delete')">Hapus</button>
    </div>
  </li>
</template>

<script>
export default {
  data() {
    return {
      isEditing: false,
      newTodoDescription: "",
    };
  },
  props: {
    description: String,
    completed: Boolean,
  },
  methods: {
    startEditing() {
      if (this.isEditing) {
        this.finishEditing();
      } else {
        this.newTodoDescription = this.description;
        this.isEditing = true;
        this.$nextTick(() => this.$refs.newTodo.focus());
      }
    },
    finishEditing() {
      this.isEditing = false;
      this.$emit("on-edit", this.newTodoDescription);
    },
  },
};
</script>

<style>
body {
  counter-reset: section;
}

.flex {
  display: flex;
  margin: 12px 0;
}

.flex:before {
  counter-increment: section;
  content: counter(section) ".";
  position: absolute;
  margin-left: -20px;
}

.descriptionBeforeEdit {
  width: 80%;
  font-size: 20px;
}

li {
  font-size: 20px;
}

.formEdit {
  width: 80%;
}

.editBtnWrap {
  width: 10%;
  text-align: center;
}

.editBtn {
  width: 50%;
  border-radius: 30px;
  background: #007bff;
  color: white;
  opacity: 0.8;
  transition: 0.3s;
}

.editBtn:hover {
  opacity: 1;
  cursor: pointer;
}

.deleteBtnWrap {
  width: 10%;
  text-align: center;
}

.deleteBtn {
  width: 50%;
  border-radius: 30px;
  background: #dc3545;
  color: white;
  opacity: 0.8;
  transition: 0.3s;
}

.deleteBtn:hover {
    opacity: 1;
    cursor: pointer;
}

.form-control {
  width: 95%;
}
</style>
