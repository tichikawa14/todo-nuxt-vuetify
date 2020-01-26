<template>
  <v-layout>
    <v-flex text-xs-center>
      <img src="/v.png" alt="Vuetify.js" class="mb-5">
      <blockquote class="blockquote">
        <h3>TODOを追加しましょう</h3>
        <v-text-field v-model="todoItemObject.title" type="text" placeholder="タイトルを入力してください"/>
        <v-text-field v-model="todoItemObject.description" type="text" placeholder="内容を入力してください"/>
        <v-btn large color="red" v-on:click="addTodo">追加する</v-btn>
        <div>
          <h3>TODO一覧</h3>
          <ul>
            <li v-for="todo in todos" v-bind:key="todo.name" v-on:click="deleteTodo(todo.id)">
              {{ todo.title }} / {{ todo.description }}
            </li>
          </ul>
        </div>
        <footer>
          <small>
            <em>&mdash;松田信介</em>
          </small>
        </footer>
      </blockquote>
    </v-flex>
  </v-layout>
</template>
​
<script>
import axios from 'axios'

export default {
  data: function () {
    return {
      todos: [],
      todoItemObject: {
        id: '',
        title: '',
        description: ''
      }
    }
  },
  created () {
    this.getTodos()
  },
  methods: {
    deleteTodo: function (id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    async getTodos () {
      try {
        var result = await axios({
          method: 'POST',
          url: 'https://limitless-bayou-12897.herokuapp.com/graphql',
          data: {
            query:
              `
              query getToDos {
                toDos {
                  id
                  title
                  description
                }
              }
            `
          }
        })
        console.log(result.data.data)
        this.todos = result.data.data.toDos
      } catch (error) {
        // console.error(error);
      }
    },
    async addTodo () {
      try {
        await axios({
          method: 'POST',
          url: 'https://limitless-bayou-12897.herokuapp.com/graphql',
          data: {
            query:
              `
              mutation {
                createToDo (input:{
                  data: {
                    title: "${this.todoItemObject.title}",
                    description: "${this.todoItemObject.description}",
                    userName: "matsuda"
                  }
                }) {
                  toDo {
                    title
                    description
                    userName
                  }
                }
              }
            `
          }
        })
        this.getTodos()
      } catch (error) {
        // console.error(error);
      }
    }
  }
}
</script>
