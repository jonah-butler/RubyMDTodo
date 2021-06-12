<template>
<div>
  <v-container>
    <v-row>
      <v-col>
        <v-card
        elevation=0>
          <v-text-field
            label="Search Assignees"
            v-model="query"
            hide-details="auto"
            @input="$emit('query', query)"
          ></v-text-field>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</div>
</template>

<script>
export default {
  data() {
    return {
      query: '',
    };
  },
}
</script>

<style>

</style>