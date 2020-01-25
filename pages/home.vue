<template>
  <v-layout>
    <v-flex text-xs-center>
      <img src="/v.png" alt="Vuetify.js" class="mb-5">
      <blockquote class="blockquote">
        <h3>ホームです</h3>
        <main-contents>
          {{ todos[0].name }} / {{ todos[0].description }}
        </main-contents>
        <footer>
          <small>
            <em>&mdash;松田信介</em>
          </small>
        </footer>
      </blockquote>
    </v-flex>
  </v-layout>
</template>
<script>
  export default {
    data: function () {
      return {
        todos: [
          {
            name: '001',
            description: 'dfaknjbtra'
          },
          {
            name: '002',
            description: '13fgreflgf'
          }
        ],
        todoItemObject: {
          name: '',
          description: ''
        }
      }
    }
  }
</script>
