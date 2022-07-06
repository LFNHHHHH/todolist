<template>
  <li @click="setChange(todo.id)">
    <label>
      <input type="checkbox" :checked='todo.done' @click="setChange(todo.id)" />
      <span>{{ todo.title }}</span>
    </label>
    <button @click.stop="delItem(todo.id)" class="btn btn-danger">删除</button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  props: ['todo'],
  methods: {
    setChange (id) {
      // this.changeCheck(id)
      this.$emit('changeCheck', id)
    },
    delItem (id) {
      if (!confirm('确定删除吗？')) return
      // this.delI(id)
      this.$emit('delI', id)
    }
  },
};
</script>

<style scoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}
li label {
  float: left;
  cursor: pointer;
}
li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}
li button {
  float: right;
  display: none;
  margin-top: 3px;
}
li:before {
  content: initial;
}
li:last-child {
  border-bottom: none;
}
li:hover {
  background-color: #ddd;
}
li:hover button {
  display: block;
}
</style>