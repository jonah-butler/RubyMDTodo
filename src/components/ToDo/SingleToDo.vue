<template>
<div>
  <v-list-item
  ref="container"
  class="todo-container"
  @click="toggleExpand">
    <v-list-item-avatar
    class="todo-avatar"
    @click="markComplete"
    :style="{
      backgroundColor: randomColor
    }">
    </v-list-item-avatar>
    <v-list-item-content
    class="todo-content">
      <v-list-item-title
      :class="(isCompleted)?'todo-title complete':'todo-title'"
      ref="title"
      >
        <h2>{{title}}</h2>
      </v-list-item-title>
      <v-list-item-title>assigned by: {{assignee}}</v-list-item-title>
      <v-list-item-subtitle
      class="description">
        {{description}}
      </v-list-item-subtitle>
    </v-list-item-content>
    <v-icon
    @click="$emit('delete', {title, assignee, description, isCompleted})"
    class="todo-delete">
      mdi-delete
    </v-icon>
  </v-list-item>

<v-divider>
</v-divider>
</div>
</template>

<script>
export default {
  data() {
    return {
      randomColor: this.generateRandomColor(),
      isCompleted: this.completed,
    };
  },
  methods: {
    toggleExpand(event) {
      event.target.classList.toggle('expand');
    },
    generateRandomColor() {
      return `#${Math.floor(Math.random()*16777215).toString(16)}`;
    },
    markComplete() {
      this.isCompleted = !this.isCompleted;
      this.$refs.title.classList.toggle('complete');
      this.$emit('update', this.isCompleted);
    },
  },
  watch: {
    completed() {
      if(typeof(this.completed) === 'function'){
        this.isCompleted = true;
      } else {
        this.isCompleted = this.completed;
      }
    },
  },
  props: {
    title: String,
    assignee: String,
    description: String,
    completed: undefined,
  },
}
</script>

<style scoped>
  .description{
    position: relative;
    bottom: -30px;
  }

  .todo-container{
    height: 75px;
    transition: all .4s ease;
    overflow: hidden;
  }

  .todo-container.expand{
    height: 300px;
  }

  .todo-container.complete{
    background-color: rgba(0,0,0,0.5) !important;
  }

  .todo-content{
    overflow: visible;
    flex: 0 0 !important;
  }

  .todo-title.complete{
    text-decoration: line-through;
  }

  .todo-avatar{
    box-shadow: 2px 2px 3px rgb(0 0 0 / 50%);
  }
  .todo-delete{
    position: absolute !important;
    top: 10px;
    right: 10px;
  }
</style>