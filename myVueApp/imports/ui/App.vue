<template>
  <div className="container">
    <header>
      <h1>Todo List</h1>
    </header>
    <ul>
      <Task v-for="(task, index) in tasks" v-bind:key="index" v-bind:task="task"  />
    </ul>
  </div>
</template>
 
<script>
import Vue from "vue";
import Task from "./Task.vue";
import { Tasks } from "../api/tasks.js";
 
export default {
  components: {
    Task
  },
  data() {
    return {};
  },
  methods: {},
  meteor: {
    tasks() {
      return Tasks.find({}).fetch();
    }
  }

};
</script>