<template>
  <div>
    <GuideText />
    <TodoList
      v-bind:key="newData"
      v-bind:setToday="setToday"
    />
    <TodoAdd
      v-bind:setToday="setToday"
      v-on:key="reRender"
    />
  </div>
</template>

<script>
require('./assets/css/ui.reset.css')

import GuideText from './components/GuideText'
import TodoList from './components/TodoList'
import TodoAdd from './components/TodoAdd'

export default {
  name: 'App',
  components: {
    GuideText,
    TodoList,
    TodoAdd
  },
  data () {
    return {
      newData: 0,
      setToday: null
    }
  },
  created () {
    this.getToday();
  },
  methods: {
    reRender () {
      this.newData = this.newData + 1
    },
    getToday () {
      const date = new Date()
      const year = date.getFullYear()
      const month = ("0" + (1 + date.getMonth())).slice(-2)
      const day = ("0" + date.getDate()).slice(-2)
      this.setToday = year + month + day
    }
  }
}
</script>

<style>
</style>
