<template>
  <div class="text-center">
    <v-btn
      class="mx-2"
      fab
      dark
      color="indigo"
      @click="overlay = !overlay"
    >
      <v-icon dark>
        mdi-plus
      </v-icon>
    </v-btn>

    <v-overlay
    v-if="overlay">
    <v-btn
      class="mx-2"
      fab
      dark
      small
      color="primary"
      @click="overlayToggle"
    >
      <v-icon dark>
        mdi-close
      </v-icon>
    </v-btn>
      <v-container>
        <v-row>
          <v-col
          cols="12"
          >
            <v-card
            class="pa-3"
            elevation=0>
              <v-text-field
              ref="assignee"
              label="Assignee"
              hide-details="auto"
              v-model="todo.assignee"
              ></v-text-field>
              <v-text-field
              ref="title"
              label="Title"
              hide-details="auto"
              v-model="todo.title"
              ></v-text-field>
              <v-textarea
              ref="description"
              v-model="todo.description"
              label="Description"
              counter
              maxlength="120"
              full-width
              single-line>
              </v-textarea>
              <v-btn
              @click="submitToDo"
              color="warning"
              dark>
              Add ToDo
            </v-btn>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-overlay>
  </div>
</template>

<script>
  export default {
    data: () => ({
      overlay: false,
      todo: {
        assignee: '',
        title: '',
        description: '',
        isCompleted: false,
      },
    }),
    methods: {
      overlayToggle() {
        this.overlay = !this.overlay;
      },
      submitToDo() {
        this.overlayToggle();
        if(this.todo.assignee.length && this.todo.title.length && this.todo.description.length){
          this.$emit('incomingToDo', {
            assignee: this.$refs.assignee.value,
            title: this.$refs.title.value,
            description: this.$refs.description.value,
            isCompleted: false,
          });     
          this.clearForm();
        }
      },
      clearForm() {
        this.todo.assignee = '';
        this.todo.title = '';
        this.todo.description = '';
      },
    },
  };
</script>

<style scoped>
  .container{
    min-width: 800px !important;
  }
</style>