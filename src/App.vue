<template>
  <div id="app" class="container-fluid">
    <div class="d-flex flex-row-reverse mt-4">
      <b-button v-b-modal.modal-new-task variant="danger">New Task</b-button>
    </div>
    <b-modal id="modal-new-task" title="Add a new todo" @ok="handleOk">
      <b-form-input
        @keyup.enter="handleOk"
        type="text"
        name="todo"
        id="todo"
        v-model="todo"
      ></b-form-input>
    </b-modal>

    <div class="container">
      <h1 class="my-4">TODO APP</h1>
      <div class="row justify-content-between">
        <div class="col-xl">
          <div class="bg-col">
            <h2>To do</h2>
            <ul>
              <draggable class="list-group" :list="todos" group="todos">
                <li
                  v-for="item in todos"
                  :key="item.id"
                  class="font-weight-bold"
                >
                  {{ item.title }}
                </li>
              </draggable>
            </ul>
          </div>
        </div>
        <div class="col-xl">
          <div class="bg-col">
            <h2>In progress</h2>
            <ul>
              <draggable class="list-group" :list="inProgress" group="todos">
                <li
                  v-for="item in inProgress"
                  :key="item.id"
                  class="font-weight-bold"
                >
                  {{ item.title }}
                </li>
              </draggable>
            </ul>
          </div>
        </div>
        <div class="col-xl">
          <div class="bg-col">
            <h2>Done</h2>
            <ul>
              <draggable class="list-group" :list="done" group="todos">
                <li
                  v-for="item in done"
                  :key="item.id"
                  class="font-weight-bold"
                >
                  {{ item.title }}
                </li>
              </draggable>
            </ul>
          </div>
        </div>
      </div>
    </div>
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
      createTodo: false,
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
  methods: {
    handleOk() {
      if (this.todo.trim() !== "") {
        this.todos.push({
          title: this.todo,
          id: uuidv4(),
        });
      }
      this.todo = "";
    },
  },
};
</script>

<style>
body {
  min-height: 100vh;
  background-image: linear-gradient(
    to right top,
    #7060b8,
    #6f67c2,
    #6d6ecd,
    #6b75d7,
    #677ce2
  );
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  box-sizing: border-box;
}
.bg-col {
  background: #f2f2f2;
  border-radius: 10px;
  margin: 20px;
  min-height: 15 0px;
}
h1 {
  color: #fff;
}
h2 {
  padding: 30px 0;
  font-weight: bold;
}
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
ul li {
  width: 90%;
  padding: 10px;
  margin: 10px auto;
  border: 1px solid #000;
  border-radius: 5px;
  background: #fff;
}
</style>
