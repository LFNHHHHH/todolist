<template>
  <div v-if="todos.length > 0" class="todo-footer">
    <label>
      <input type="checkbox" v-model="checked" />
    </label>
    <span> <span>已完成{{ checkedNum }}</span> / 全部{{ todos.length }} </span>
    <button @click="clearDown" class="btn btn-danger">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ['todos', 'changeAll', 'clearD'],
  computed: {
    checkedNum () {
      let list = this.todos.filter(item => item.done)
      return list.length
    },
    checked: {
      get () {
        return this.checkedNum == this.todos.length && this.todos.length > 0
      },
      set (val) {
        this.changeAll(val)
      }
    }
  },
  methods: {  
    clearDown () {
      this.clearD()
    },
    changeCheck (e) {
      if (e.target.checked) {
        this.checkAll()
      } else {
        this.clearAll()
      }
    }
  }
};
</script>

<style scoped>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}
.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}
.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}
.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>