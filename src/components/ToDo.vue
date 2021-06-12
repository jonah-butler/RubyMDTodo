<template>
  <v-app id="todo">
    <img
    id="logo"
    src="http://www.rubymd.io/images/logoTransparent.png"
    alt="">
    <Search 
    :query ="query"
    v-on:query="filterByName"/>
    <New
    v-on:incomingToDo="addToDo"/>
    <v-system-bar app>
      <v-spacer></v-spacer>
    </v-system-bar>
    <v-main>
      <v-container
        class="py-8 px-6"
        fluid
      >
        <v-row>
          <v-col
            v-for="card in cards"
            :key="card"
            cols="12"
          >
            <v-card>
              <v-subheader>{{ card }}</v-subheader>
              <v-list v-if="todos.length && !query.length"
              two-line>
                <ToDo
                v-for="(todo, index) in todos"
                :title="todo.title"
                :assignee="todo.assignee"
                :description="todo.description"
                :completed="todo.isCompleted"
                @update="todo.isCompleted = $event"
                @delete="deleteTodo"
                :key="index"/>
              </v-list>
              <v-list v-else-if="query.length && filteredToDos.length"
              two-line>
                <ToDo
                v-for="(todo, index) in filteredToDos"
                :title="todo.title"
                :assignee="todo.assignee"
                :description="todo.description"
                :completed="todo.isCompleted"
                @delete="deleteTodo"
                @update="todo.isCompleted = $event"
                :key="index"/>
              </v-list>
              <v-list v-else
              two-line>
                No Todos
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Search from '@/components/ToDo/Search.vue';
import New from '@/components/ToDo/NewToDo.vue';
import ToDo from '@/components/ToDo/SingleToDo.vue';

  export default {
    components: {
      Search,
      New,
      ToDo,
    },
    data() {
      return {
        cards: ['Todos'],
        query: '',
        todos: [],
        filteredToDos: [],
      };
    },
    methods: {
      addToDo(value) {
        let newToDo = value;
        this.todos.push(newToDo);
      },
      deleteTodo($event) {
        this.todos.forEach((todo, i) => {
          if(this.deleteFilter(todo, $event)){
            this.todos.splice(i,1);
          }
        })
        if(this.filteredToDos.length){
          this.filteredToDos.forEach((todo, i) => {
          if(this.deleteFilter(todo, $event)){
            this.filteredToDos.splice(i,1);
          }
        })
        }
      },
      deleteFilter(todo, $event) {
        if(todo.assignee === $event.assignee && todo.description === $event.description && todo.isCompleted === $event.isCompleted && todo.title === $event.title){
            return true;
          }
      },
      filterByName($event) {
        this.query = $event;
        if($event != ''){
          const regEx = new RegExp(`\\b${$event}`, 'i');
          this.filteredToDos = this.todos.filter((todo) => {
            return todo.assignee.match(regEx);
          })
        }
      },
    },
  }
</script>

<style scoped>
  #logo{
    max-width: 400px;
  }
</style>
