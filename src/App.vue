<template>
  <div id="app" class="container">
    <h1>TODO APP</h1>
    <b-card-group deck>
      <b-card column header="To do" text-variant="success">
        <draggable class="list-group" :list="todos" group="todos">
          <b-list-group-item v-for="item in todos" :key="item.id">{{
            item.title
          }}</b-list-group-item>
        </draggable>
      </b-card>
      <b-card column header="In progress">
        <draggable class="list-group" :list="inProgress" group="todos">
          <b-list-group-item v-for="item in inProgress" :key="item.id">{{
            item.title
          }}</b-list-group-item>
        </draggable>
      </b-card>
      <b-card column header="Done">
        <draggable class="list-group" :list="done" group="todos">
          <b-list-group-item v-for="item in done" :key="item.id">{{
            item.title
          }}</b-list-group-item>
        </draggable>
      </b-card>
    </b-card-group>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
import draggable from "vuedraggable";

export default {
  name: "App",
  components: {
    draggable,
  },
  data() {
    return {
      todo: "",
      todos: [
        {
          title: "todo",
          id: uuidv4(),
        },
      ],
      inProgress: [
        {
          title: "progress",
          id: uuidv4(),
        },
      ],
      done: [
        {
          title: "done",
          id: uuidv4(),
        },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
