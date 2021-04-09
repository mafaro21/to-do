<template>
  <div id="app">
    <div>
      <button @click="toggleTheme">{{ toggleText }}</button>
      <h1>TO-DO LIST</h1>

      <div class="back">
        <form @submit.prevent="addTodo">
          <input
            v-model="newTodo"
            type="text"
            placeholder="Enter a Task"
            autocomplete="on"
            required
            v-on:input="disable"
          />

          <button type="sumbit" :class="{ disablebtn: isDisabled }">Add</button>
        </form>

        <div class="to-do" v-for="(todo, index) in todos" :key="todo.id">
          <li :class="{ done: todo.done }" @click="toggleDone(todo, index)">
            {{ todo.content }}
          </li>
        </div>

        <div v-if="this.todos.length === 0" class="empty">
          Your To-Do List is Empty
        </div>
        <button v-else @click="removeAll" class="remove">Remove All</button>
      </div>
    </div>
  </div>

  <footer>
    <!-- <div>DONE BY MAFARO, </div> -->
    <div>BUILT WITH VUE.JS</div>
    <a href="https://v3.vuejs.org/"><img :src="img" /></a>
  </footer>
</template>



<script>
import { ref } from "vue";
import img from "./vuelogo.png";

export default {
  name: "App",
  data() {
    const newTodo = ref("");
    const todos = ref([]);

    return {
      newTodo,
      todos,
      img: img,
      text: "",
      theme: "",
      toggleText: "light mode",
      isDisabled: false,
    };
  },

  methods: {
    addTodo() {
      //add new item to todo list
      this.todos.push({
        id: Date.now(),
        done: false,
        content: this.newTodo,
      });

      this.newTodo = "";
    },

    toggleDone(todo) {
      // , index
      //mark todo as done
      todo.done = !todo.done;

      if (todo.done === true) {
        //remove after 10 seconds
        // setTimeout(() => {
        //   console.log("deleted");
        //   this.todos.splice(index, 1);
        // }, 10000);
      }
    },

    disable() {
      //disale button when field is empty(hopefully)
      if (this.newTodo.length < 3) {
        this.isDisabled = true;
      } else {
        this.isDisabled = false;
      }
    },

    removeAll() {
      //remove all current todos
      this.todos = [];
      this.newTodo = "";
    },

    toggleTheme() {
      this.theme = this.theme == "lightMode" ? "" : "lightMode";
      document.documentElement.setAttribute("data-theme", this.theme);
      // sessionStorage.setItem("mode", this.theme);

      if (this.theme === "") {
        this.toggleText = "light mode";
      } else {
        this.toggleText = "dark mode";
      }
    },
  },

  // mounted() {
  //   sessionStorage.setItem("mode", this.theme);
  // },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Comfortaa&display=swap");

* {
  font-family: "Comfortaa", cursive, sans-serif;
  text-align: center;
  color: white;
  max-height: 100vh;
  max-width: 100vw;
}
body {
  background-color: #1f2970;
  padding: 0;
  margin: 0;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
  transition: all 1s ease-in-out;
}

.back {
  background-color: #347fb1;
  border-radius: 15px;
  z-index: 1;
  padding: 25px;
  width: 50%;
  margin: auto;
  filter: drop-shadow(10px 9px 5px #4444dd);
}

.to-do {
  margin-top: 13px;
  padding: 2px;
}
.to-do:hover {
  cursor: pointer;
}
.empty {
  margin-top: 2%;
  padding: 5%;
}
.remove {
  margin-top: 2%;
}
.done {
  text-decoration: line-through;
}
.disablebtn {
  display: none;
}
li {
  transition: all 2s ease-in-out;
}
input {
  padding: 12px;
  border-radius: 15px;
  width: 70%;
  font-size: 16px;
  border: 1px solid black;
  background-color: #1f2970;
  color: white;
}
input:focus,
button:focus {
  outline: none;
}

button {
  margin-left: 6px;
  padding: 12px;
  border-radius: 15px;
  border: 1px solid black;
  background-color: #55b09b;
  transition: all 1s ease-in-out;
}
button:hover {
  cursor: pointer;
  transform: scale(1.1);
}

footer {
  bottom: 0;
  position: fixed;
  margin-bottom: -10px;
  background-color: #55b09b;
  text-align: center;
  justify-items: center;
  width: 100vw;
  padding: 20px;
}
img {
  background-color: #646da9;
  border-radius: 50%;
  width: 40px;
  padding: 5px;
  transition: all 0.1s ease-in-out !important;
}
img:hover {
  transform: scale(1.1);
}

[data-theme="lightMode"] * {
  color: #1f2970;
  transition: all 1s ease-in-out;
}

[data-theme="lightMode"] body {
  background-color: #f4f4f5;
  color: white;
}

[data-theme="lightMode"] input {
  color: #1f2970;
  background-color: #f4f4f5;
}

[data-theme="lightMode"] .back {
  background-color: #56afd0;
}

[data-theme="lightMode"] li {
  transition: all 2s ease-in-out;
}
</style>
