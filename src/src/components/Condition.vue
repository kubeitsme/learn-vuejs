<template>
  <div class="condition">
    <h1>{{ header }}</h1>
    <div>
      <p>{{ msg }}</p>
      <button v-on:click="reverseMessage">Reverse Message</button>
    </div>
    <span v-bind:title="title"></span>
    <div>
      <p v-if="seen">Thoát ẩn thoát hiện</p>
      <button v-on:click="showHide">{{ buttonSeen }}</button>
    </div>
    <ol>
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.text }}
      </li>
    </ol>
    <div>
      <input type="text" name="item" v-model="item"><br>
      <button v-on:click="addToList">Add to list</button>
      <button v-on:click="removeAll">Remove all</button>
    </div>
    <div>
      <h4>component</h4>
      <ul v-if="todos.length">
        <TodoListItem
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          @remove="removeTodo"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import TodoListItem from './TodoListItem.vue'

export default {
  name: 'Condition',
  components: {
    TodoListItem
  },
  data () {
    return {
      header: 'Condition page',
      msg: 'Do you wanna build a Vue app ?',
      title: 'Bạn đã mở trang này vào ' + new Date().toLocaleString(),
      seen: true,
      buttonSeen: 'Hide',
      item: '',
      todos: [
        { id: 1, text: 'Học JavaScript' },
        { id: 2, text: 'Học Vue' },
        { id: 3, text: 'Xây dựng cái gì đó hay ho' }
      ]
    }
  },
  methods: {
    reverseMessage: function(){
      this.msg = this.msg.split(' ').reverse().join(' ')
    },
    showHide: function(){
      this.seen = this.seen ? false : true
      this.buttonSeen = this.seen ? 'Hide' : 'Show'
    },
    addToList: function(){
      this.todos.push({text: this.item})
      this.item = ''
    },
    removeAll: function(){
      this.todos = []
    },
    removeTodo: function(){
      console.log('removeTodo')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
