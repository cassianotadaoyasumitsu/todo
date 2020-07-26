<template>
  <div>
    <input
      type="text"
      class="todo-input"
      placeholder="Add to List"
      v-model="newToDo"
      @keyup.enter="addTodo"
    />
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      <div class="todo-left">
        <input type="checkbox" v-model="todo.completed" />
        <div
          v-if="!todo.editing"
          @dblclick="editTodo(todo)"
          class="todo-label"
          :class="{ completed : todo.completed }"
        >{{todo.title}}</div>
        <input
          v-else
          class="todo-edit"
          type="text"
          v-model="todo.title"
          @blur="doneEdit(todo)"
          @keyup.enter="doneEdit(todo)"
          @keyup.esc="cancelEdit(todo)"
          v-focus
        />
      </div>
      <div class="remove" @click="removeTodo(index)">&times;</div>
    </div>
    <hr>
    <div class="items-left">You have {{ remaining }} tasks.</div>
  </div>
</template>

<script>
export default {
  name: "ToDo",
  data() {
    return {
      newToDo: "",
      idForTodo: 3,
      beforeEditCache: "",
      todos: [
        {
          id: 1,
          title: "Vue",
          completed: false,
          editing: false,
        },
        {
          id: 2,
          title: "JS",
          completed: false,
          editing: false,
        },
      ],
    };
  },

  computed: {
    //filter by not completed tasks
    remaining() {
      return this.todos.filter(todo => !todo.completed).length;
    }
  },

  directives: {
    focus: {
      inserted: function (el) {
        el.focus();
      },
    },
  },

  methods: {
    addTodo() {
      //disable empty inserts .trim remove whitespace from ends
      if (this.newToDo.trim().length == 0) {
        return;
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newToDo,
        completed: false,
      });

      this.newToDo = "";
      this.idForTodo++;
    },
    //edit ToDo
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    doneEdit(todo) {
      //prevent empty edit
      if (todo.title.trim() == "") {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false;
    },
    cancelEdit(todo) {
      //cancel edit by esc
      todo.title = this.beforeEditCache;
      todo.editing = false;
    },
    //remove ToDo
    removeTodo(index) {
      //confirm delete by alert
      confirm('Are you sure?') ? this.todos.splice(index, 1) : cancelEdit(todo);      
    },
  },
};
</script>

<style>
.todo-input {
  width: 100%;
  padding: 10px 16px;
  font-size: 16px;
  margin: 16px 0 16px 0;
  border-radius: 8px;
}

.todo-item {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 24px 0 24px;
}

.remove {
  cursor: pointer;
  font-size: 32px;
}

.todo-left {
  display: flex;
  align-items: center;
}

.todo-label {
  padding: 12px;
  border: 1px solid white;
  margin-left: 12px;
}

.todo-edit {
  font-size: 24px;
  margin-left: 12px;
  padding: 12px;
  border: 1px solid lightgray;
  border-radius: 4px;
}

.completed {
  text-decoration: line-through;
  color: grey;
}

.items-left {
  display: flex;
  justify-content: left;
  margin-top: 12px;
}
</style>
