<script setup>
import { reactive, defineEmits } from "vue";

const emit = defineEmits(["create-todo"]);
const todoState = reactive({
  todo: "",
  invalid: null,
  errMsg: "",
});

/* const todoState = reactive({
  todo: "Test",
});

Pour accéder à todo dans v-model => v-model="todoState.todo"

*/
const createTodo = () => {
  todoState.invalid = null;
  if (todoState.todo !== "") {
    emit("create-todo", todoState.todo);
    todoState.todo = "";
    return;
  }
  todoState.invalid = true;
  todoState.errMsg = "Texte manquant !";
};
</script>

<template>
  <div class="input-wrap" :class="{ 'input-err': todoState.invalid }">
    <input
      type="text"
      placeholder="Ajouter une tâche..."
      v-model="todoState.todo"
    />
    <button @click="createTodo">Ajouter</button>
  </div>

  <!-- <p v-if="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p> -->

  <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
</template>

<style lang="scss" scoped>
.input-wrap {
  transition: 250ms ease;
  display: flex;
  border: 2px solid #f1f1f1;

  &.input-err {
    border-color: red;
  }

  input {
    font-family: "Amatic SC", cursive;
    font-size: 20px;
    width: 100%;
    height: 30px;
    padding: 8px 6px;
    border: none;
    cursor: pointer;
    &:focus {
      outline: none;
    }
  }
  button {
    font-family: "Amatic SC", cursive;
    font-weight: bold;
    font-size: 20px;
    border: none;
    padding: 8px 16px;
    cursor: pointer;
  }
}
.err-msg {
  margin-top: 6px;
  font-size: 12px;
  color: red;
  text-align: center;
}
</style>
