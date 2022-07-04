<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo" />
        <MyList :todos="todos" :changeCheck="changeCheck" :delI="delI" />
        <MyFooter :todos="todos" :changeAll="changeAll" :clearD="clearD" />
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader";
import MyList from "./components/MyList";
import MyFooter from "./components/MyFooter.vue";

export default {
  name: "App",
  components: { MyHeader, MyList, MyFooter },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem('todos')) || [],
    };
  },
  watch: {
    todos: {
      deep: true,
      handler (val) {
        localStorage.setItem('todos', JSON.stringify(val))
      }
    }
  },
  methods: {
    addTodo (todo) { // 获取子组件数据
      this.todos.unshift(todo)
    },
    changeCheck (id) {
      this.todos.forEach(item => {
        if (item.id == id) item.done = !item.done
      })
    },
    delI (id) {
      let index = this.todos.findIndex(item => item.id == id)
      this.todos.splice(index, 1)
    },
    changeAll (checked) {
      this.todos.forEach(item => {
        item.done = checked
      })
    },
    clearD () {
      this.todos = this.todos.filter (item => !item.done)
    }
  },
};
</script>

<style>
body {
  background: #fff;
}
.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}
.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn:focus {
  outline: none;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
