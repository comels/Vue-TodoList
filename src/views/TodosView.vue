<script setup>
import { Icon } from "@iconify/vue";
import { ref, watch, computed } from "vue";
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";
import { uid } from "uid";

const todoList = ref([]);

watch(
  todoList,
  () => {
    setTodoListLocalStorage();
  },
  {
    deep: true,
  }
);

const todoComputed = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});

const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
  if (savedTodoList) {
    todoList.value = savedTodoList;
  }
};

fetchTodoList();

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};

const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
};

const toggleEditTodo = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
};

const updateTodo = (todoVal, todoPos) => {
  todoList.value[todoPos].todo = todoVal;
};

const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
};
</script>

<template>
  <main>
    <TodoCreator @create-todo="createTodo" />
    <ul v-if="todoList.length > 0" class="todo-list">
      <TodoItem
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        @edit-todo="toggleEditTodo"
        @toggle-complete="toggleTodoComplete"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
      />
    </ul>
    <p v-else class="todo-msg">
      <Icon icon="icon-park-solid:good-one" color="#21177d" width="22" />
      <span>Tu n'as rien à faire !</span>
    </p>
    <p v-if="todoComputed && todoList.length > 0" class="todo-msg">
      <Icon icon="noto-v1:party-popper" />
      <span>Bravo !</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 550px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    text-align: center;
    margin-bottom: 16px;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  ul {
    margin: 0;
    padding: 0;
  }
  .todo-msg {
    display: flex;
    font-size: 20px;
    font-weight: bold;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
