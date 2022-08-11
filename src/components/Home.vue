<template>
  <div class="container">
    <div class="todo">
      <h1 class="title">Todo App</h1>
      <div class="todo-input">
        <input
          type="text"
          v-model="name"
          @keyup.enter="handleClick()"
          v-autofocus
        />
        <button @click="handleClick" class="btn">Add</button>
        <button @click="tonggleFilter" class="btn">Filter</button>
      </div>
      <div class="todo-list">
        <h3 v-for="(todo, index) in filters" :key="index" class="todo-item">
          <input
            type="checkbox"
            v-model="todo.isDone"
            @click="todo.isDone = !todo.isDone"
            class="checkbox"
          />
          <span :class="{ 'active-todo': todo.isDone }">{{ todo.text }}</span>
          <span class="btn-close" @click="handleDelete(index)">&times;</span>
        </h3>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name: "",
      isFilter: false,
      todos: [],
    };
  },
  methods: {
    handleClick() {
      if (this.name === "") {
        alert("Please enter a to-do");
      } else {
        this.todos.push({ text: this.name, isDone: false });
        this.name = "";
      }
    },
    handleDelete(index) {
      this.todos.splice(index, 1);
    },
    tonggleFilter() {
      this.isFilter = !this.isFilter;
    },
  },
  directives: {
    autofocus: {
      inserted(el) {
        el.focus();
      },
    },
  },
  computed: {
    filters() {
      if (!this.isFilter) {
        return this.todos;
      } else {
        return this.todos.filter((todo) => todo.isDone);
      }
    },
  },
};
</script>
<style>
.todo {
  text-align: center;
}

.title {
  margin: 20px 0;
}

.todo input {
  font-size: 20px;
  border: 2px solid #ccc;
  outline: none;
  border-radius: 4px;
}

.btn {
  margin-left: 5px;
  padding: 4px 16px;
  border: 2px solid #ccc;
  border-radius: 4px;
}

.btn:hover {
  cursor: pointer;
  background-color: pink;
  color: #fff;
}

.todo-input {
  display: flex;
  align-items: center;
  justify-content: center;
}

.todo-item {
  font-size: 18px;
  margin-top: 10px;
}

.active-todo {
  text-decoration: line-through;
}

.checkbox {
  margin-right: 15px;
}

.todo-list {
  text-align: left;
  margin-left: 373px;
}

.btn-close {
  margin-left: 10px;
  padding: 0 16px;
}

.btn-close:hover {
  cursor: pointer;
  color: #ccc;
}
</style>
