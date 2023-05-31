<script setup>
import { Icon } from "@iconify/vue";
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  },
});
defineEmits(["toggle-complete", "edit-todo", "completed-todo", "delete-todo"]);
</script>

<template>
  <li>
    <input
      type="checkbox"
      @input="$emit('toggle-complete', index)"
      :checked="todo.isCompleted"
    />
    <div class="todo">
      <input
        v-if="todo.isEditing"
        type="text"
        :value="todo.todo"
        @input="$emit('update-todo', $event.target.value, index)"
      />
      <span v-else :class="{ 'completed-todo': todo.isCompleted }">
        {{ todo.todo }}
      </span>
    </div>
    <div class="todo-actions">
      <Icon
        v-if="todo.isEditing"
        icon="ph:check-circle"
        class="icon"
        color="21177D"
        width="22"
        @click="$emit('edit-todo', index)"
      />
      <Icon
        v-else
        icon="ph:pencil-fill"
        class="icon"
        color="21177D"
        width="22"
        @click="$emit('edit-todo', index)"
      />
      <Icon
        icon="ph:trash"
        class="icon"
        color="f95e5e"
        width="22"
        @click="$emit('delete-todo', todo.id)"
      />
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  display: flex;
  align-items: center;
  gap: 30px;
  padding: 16px 10px;
  background-color: #f1f1f1;

  input[type="checkbox"] {
    appearance: none;
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50%;
    &:checked {
      background-color: #21177d;
    }
  }

  .todo {
    flex: 1;
    font-size: 20px;

    .completed-todo {
      text-decoration: line-through;
    }

    input[type="text"] {
      width: 100%;
      padding: 2px 6px;
      border: 2px solid #21177d;
    }
  }
  .todo-actions {
    display: flex;
    gap: 6px;
    transition: 150ms ease-in-out;
    .icon {
      cursor: pointer;
    }
  }
}
</style>
