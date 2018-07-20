<template>
  <li>
    <input type="text" ref="input" :value="content" :disabled="bool" />
    <button class="change" @click="getFocus">{{msg1}}</button>
    <button class="del" @click="handleClick">删除</button>
  </li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: ['content', 'index'],
  data: function () {
    return {
      bool: true,
      msg1: '修改'
    }
  },
  methods: {
    handleClick: function () {
      this.$emit('delete', this.index)
    },
    getFocus: function () {
      if (this.bool) {
        this.bool = false
        this.$nextTick(function () {
          this.$refs.input.focus()
          this.msg1 = '确定'
        })
      } else {
        console.log(this.$refs.input.value)
        this.$emit('edit', this.index, this.$refs.input.value)
        this.msg1 = '修改'
        this.bool = true
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
