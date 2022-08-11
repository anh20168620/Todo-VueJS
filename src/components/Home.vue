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
        <button @click="handleFilter" class="btn">Filter</button>
      </div>
      <div v-if="!isShow" class="todo-list">
        <h3 v-for="(todo, index) in todos" :key="index" class="todo-item">
          <input
            type="checkbox"
            v-model="todo.done"
            @click="todo.done = !todo.done"
            class="checkbox"
          />
          <span :class="{ active_todo: todo.done }">{{ todo.text }}</span>
          <span class="btn-close" @click="handleDelete(index)">&times;</span>
        </h3>
      </div>
      <div v-else class="todo-list">
        <h3 v-for="(filter, index) in filters" :key="index" class="todo-item">
          <input
            type="checkbox"
            v-model="filter.done"
            @click="filter.done = !filter.done"
            class="checkbox"
          />
          <span :class="{ active_todo: filter.done }">{{ filter.text }}</span>
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
      isShow: false,
      filters: [],
      todos: [],
    };
  },
  methods: {
    handleClick() {
      if (this.name == "") {
        alert("Please enter a to-do");
      } else {
        this.todos.push({ text: this.name, done: false });
        this.name = "";
      }
    },
    handleDelete(index) {
      this.todos.splice(index, 1);
      this.filters.splice(index, 1);
    },
    handleFilter() {
      this.filters = [];
      this.isShow = !this.isShow;
      this.filters.push(...this.todos.filter((todo) => todo.done == true));
    },
  },
  directives: {
    autofocus: {
      inserted(el) {
        el.focus();
      },
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

.active_todo {
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
