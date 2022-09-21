<template>
  <section class="board-info-bar">
    <Header />
  </section>
  <!-- {{ items }} -->
  <Board v-bind:propsdata="items" />
  <Footer />
  <button @click="fetchData">Data</button>
</template>

<script>
import Header from "./components/TrelloHeader.vue";
import Board from "./components/TrelloBoard.vue";
import Footer from "./components/TrelloFooter.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    Board,
    Footer
  },
  data() {
    return {
      items: [],
    };
  },
  mounted() {
    axios
      .get("./dummy/dummy.json")
      .then((response) => (this.items = response.data.board[0]))
      .catch((error) => (console.log(error)))
      .then(() =>(console.log("axios 실행")));
  },
  methods: {
    fetchData() {
      console.log(this.items);
    }
  },
  // created() {
  //   if (localStorage.length > 0) {
  //     for (let i = 0; i < localStorage.length; i++) {
  //       if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
  //         localStorage.getItem(localStorage.key(i));
  //         console.log(JSON.parse(localStorage.getItem(localStorage.key(i))));
  //         this.todoItems.push(
  //           JSON.parse(localStorage.getItem(localStorage.key(i)))
  //         );
  //         // this.todoItems.push(localStorage.key(i));
  //       }
  //     }
  //   }
  // }
};
</script>

<style>
:root {
  font-size: 10px;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  display: flex;
  flex-direction: column;
  background-color: #868e96;
}

.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  font: inherit;
  background: none;
  border: none;
  color: inherit;
  padding: 0;
  cursor: pointer;
}

:focus {
  outline-color: #fa0;
}

.board-info-bar {
  flex-basis: 3rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 0.8rem 0;
  padding: 0 1rem;
  color: #ffffff;
}
</style>