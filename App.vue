<template>
  <div id="app">
    <h1 v-text='title'></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for='(item, index) in items' v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
        {{item.label}}<button v-on:click="removeItem(index)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store'
console.log(Store)
export default {
  data: function () {
    return {
      title: 'This is a todo list!',
      items: Store.fetch(),
      newItem: ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem = ''
    },
    removeItem: function (index) {
      this.items.splice(index, 1)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: auto;
  margin-top: 60px;
  width: 300px;
  
}
input {
  margin-bottom: 10px;
  length:10px;
}
ul {
  width: 300px;
  margin: auto;
}
ul li {
  margin-left: 10px;
}
.finished {
  text-decoration: underline;
}
</style>
