<script setup>
import { reactive } from 'vue';
import TodoButton from './TodoButton.vue';

const emit = defineEmits(['create-todo']);

// const todo = ref('');

const todoState = reactive({
    todo: '',
    invalid: null,
    errMsg: '',
})

const createTodo = () => {
    todoState.invalid = null;
    if (todoState.todo !== '') {
        emit('create-todo', todoState.todo);
        todoState.todo = '';
        return;
    }
    todoState.invalid = true;
    todoState.errMsg = 'The todo cannot be empty.';
};

</script>

<template>
    <div class="input-wrap" :class="{'input-err' : todoState.invalid}">
        <!-- :class is shorthand for applying styling conditionally -->
        <input type="text" v-model="todoState.todo">
        <TodoButton @click="createTodo()" />
        <!-- Could have opening and closing tags, with custom text between as normal -->
        <!-- @click is shorthand for v-on:click -->
    </div>
    <!-- <p v-if="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p> -->
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
    <!-- Both these will work in this case, to show the error message paragraph below.
    In more complex cases, choose based on:
    1. v-if will recreate the element each time - better if this is going to be used once or infrequently
    2. v-show will just toggle the CSS display property to show or hide it - best for if the toggle is going to be used a lot -->
</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

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

    &:focus {
      outline: none;
    }
  }
}

.err-msg {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: red;
}
</style>