<template>
 <div class="todo-item">
    <div class="todo-item-left">
                <input v-model="completed" type="checkbox" />
                <div
                    v-if="!editting"
                    @dblclick="editTodo()"
                    class="todo-item-label"
                    :class="{ completed: completed }"
                >
                    {{ title }}
                </div>
                <input
                    v-else
                    class="todo-item-edit"
                    type="text"
                    v-model="title"
                    @blur="doneEdit()"
                    @keyup.enter="doneEdit()"
                    @keyup.esc="cancelEdit()"
                    v-focus
                />
            </div>
            <div class="remove-item" @click="removeTodo(index)">
                <div class="icon-trash" style="float: left">
                    <div
                        class="trash-lid"
                        style="background-color: #2cc3b5"
                    ></div>
                    <div
                        class="trash-container"
                        style="background-color: #2cc3b5"
                    ></div>
                    <div class="trash-line-1"></div>
                    <div class="trash-line-2"></div>
                    <div class="trash-line-3"></div>
                </div>
            </div>
 </div>
</template>

<script>
   export default {
  name: 'todo-item',
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
        'id': this.todo.id,
        'title': this.todo.title,
        'completed': this.todo.completed,
        'editting': false,
        'lastTitle': '',
    }
  },
  methods: {
    removeTodo(index){
        this.$emit('removeTodo', index);
    }
  },
}
</script>