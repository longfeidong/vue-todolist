<template>
  <div id="app">
    <div>
      <input type="text" v-model="inputValue" @keyup.enter="handleSubmit" placeholder="请输入……">
      <button @click="handleSubmit">提交</button>
    </div>
    <ul>
      <todo-item v-for="(item, index) in lists" :content="item" :key="index" :index="index" @delete="handleDelete" @edit="handleEdit"></todo-item>
    </ul>
    <p>{{lists}}</p>
    <p>共{{number}}条</p>
    <div><button @click="reverse">翻转</button><button @click="sort">排序</button></div>
  </div>
</template>

<script>
import TodoItem from './components/TodoItem'

export default {
  name: 'App',
  components: {
    'todo-item': TodoItem
  },
  data: function () {
    return {
      inputValue: '',
      lists: [],
      num: 0,
      message: 'hello'
    }
  },
  computed: {
    number: {
      get: function () {
        return this.lists.length
      }
    }
  },
  methods: {
    handleSubmit: function () {
      this.lists.push(this.inputValue)
      this.inputValue = ''
      // this.num = this.lists.length
    },
    handleDelete: function (index) {
      this.lists.splice(index, 1)
      // this.num = this.lists.length
    },
    handleEdit: function (index, content) {
      this.lists.splice(index, 1, content)
    },
    reverse: function () {
      this.lists.reverse()
    },
    sortNumber: function (a, b) {
      return a - b
    },
    sort: function () {
      this.lists.sort(this.sortNumber)
    }
  },
  beforeCreate: function () {
    console.log('beforeCreate')
  },
  created: function () {
    console.log('created阶段实例还未挂载' + ' -> this.$el: ' + this.$el)
  },
  beforeMount: function () {
    console.log(this.$el)
    console.log('beforeMount挂载开始之前被调用' + this.$el)
  },
  mounted: function () {
    console.log(this.$el)
    console.log('mounted实例被挂载后调用，el被vm.$el替换 ' + this.$el)
  },
  beforeUpdate: function () {
    console.log(this.lists)
    console.log('数据更新时beforeUpdate被调用')
  },
  updated: function () {
    console.log(this.lists)
    console.log('数据更新后虚拟DOM重新渲染之后updated会被调用')
  }
}
</script>

<style>

</style>
