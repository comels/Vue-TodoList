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
    <input type="text" v-model="todoState.todo" />
    <button @click="createTodo">Ajouter</button>
  </div>

  <!-- <p v-if="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p> -->

  <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
</template>

<style lang="scss" scoped>
.input-wrap {
  transition: 250ms ease;
  display: flex;
  border: 2px solid rgb(24, 145, 28);

  &.input-err {
    border-color: red;
  }

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;
    cursor: pointer;
    &:focus {
      outline: none;
    }
  }
  button {
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
