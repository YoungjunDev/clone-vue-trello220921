<!--HTML-->
<template>
  <div class="list" v-for="board in board" v-bind:key="board">
    <div class="title-menu">
      <!-- {{ board.list_title }} -->
      <span>
        <h3
          class="list-title"
          v-show="board.list_title.titleChangeh3"
          @click="changeTitle(board)"
        >
          {{ board.list_title.listTitle }}
        </h3>
      </span>
      <input
        class="list-title-input"
        v-show="board.list_title.titleChangeInput"
        :value="board.list_title.listTitle"
        @blur="closeTitle(board)"
      />
      <button class="action-menu">
        <i class="fa-solid fa-ellipsis"></i>
      </button>
    </div>
    <Card v-bind:card="board.list_item" />
    <div class="list-card-labels" v-show="board.list_title.addCardDiv">
      <textarea
        name=""
        id="list-card-composer-textarea"
        cols="26"
        rows="10"
        placeholder=" Enter a title for this card..."
        v-model="newlistItem"
        v-on:keyup.enter="addTitle"
      ></textarea>
      <div class="list-update-col">
        <button class="add-card-update-btn">Add card</button>
        <span class="add-list-close" @click="closeCard(board)">
          <i class="fa-solid fa-x"></i>
        </span>
      </div>
    </div>
    <button
      class="add-card-btn btn"
      @click="addCard(board)"
      v-show="board.list_title.addCardBtn"
    >
      &#43;Add a card
    </button>
  </div>
</template>

<!-- script -->
<script>
import Card from "./TrelloCard.vue";

export default {
  name: "TrelloList",
  props: ["board"],
  data() {
    return {
      updateTitle: "",
    };
  },
  methods: {
    addTitle: function () {
      console.log(this.newTitleItem);
    },

    changeTitle: function (board) {
      board.list_title.titleChangeh3 = !board.list_title.titleChangeh3;
      board.list_title.titleChangeInput = !board.list_title.titleChangeInput;
      this.$refs.cursor.focus();
    },

    closeTitle: function (board) {
      board.list_title.titleChangeh3 = !board.list_title.titleChangeh3;
      board.list_title.titleChangeInput = !board.list_title.titleChangeInput;
    },

    addCard: function (board) {
      console.log(board.list_title.addCardDiv);
      board.list_title.addCardDiv = !board.list_title.addCardDiv;
      board.list_title.addCardBtn = !board.list_title.addCardBtn;
    },

    closeCard(board) {
      board.list_title.addCardDiv = !board.list_title.addCardDiv;
      board.list_title.addCardBtn = !board.list_title.addCardBtn;
    },
  },
  components: {
    Card,
  },
};
</script>

<!-- css -->
<style scoped>
.list {
  flex: 0 0 27rem;
  display: flex;
  flex-direction: column;
  background-color: #e2e4e6;
  max-height: calc(100vh - 11.8rem);
  border-radius: 0.5rem;
  margin-right: 1rem;
  box-shadow: 0px 0px 10px #000000;
}
/* .list:last-of-type {
    margin-right: 0;
  } */

.title-menu {
  display: flex;
  margin-top: 0.1rem;
  margin-bottom: 0.1rem;
  margin-right: 1rem;
  margin-left: 0.1rem;
  justify-content: space-between;
}

.action-menu {
  height: 100%;
  margin: auto 0;
  border: none;
  background-color: #e2e4e6;
}

.action-menu:hover {
  background-color: #cdd2d4;
  color: #4d4d4d;
  text-decoration: none;
}

.list-title,
.list-title-input {
  font-size: 1.4rem;
  font-weight: 700;
  color: #333;
  padding: 1rem;
  margin-top: 0.1rem;
  margin-bottom: 0.1rem;
  margin-top: 1rem;
}

.list-title-input {
  border-radius: 0rem;
  border-color: #4682b4;
  margin: 0.2rem 1rem;
  height: 2em;
  margin-top: 1rem;
}
.list-card-labels {
  overflow: auto;
  position: relative;
  padding: 0px 5px;
}

.list-update-col {
  display: flex;
}

#list-card-composer-textarea {
  overflow: hidden;
  overflow-wrap: break-word;
  resize: none;
  height: 54px;
  font-family: Verdana, Geneva, sans-serif;
  font-size: 16px;
  border-radius: 0.4rem;
  border: none;
}

.add-card-update-btn {
  margin: 5px;
  padding: 8px;
  background-color: #4b89dc;
  border: none;
  border-radius: 0.3rem;
  color: white;
  cursor: pointer;
}

.add-card-update-btn:hover {
  background-color: #0067a3;
  color: white;
  text-decoration: none;
}

.add-list-close {
  height: 100%;
  margin: 10px;
  cursor: pointer;
}

.fa-x {
  font-size: 20px;
  color: #4d4d4d;
}

.fa-x:hover {
  color: #000000;
  text-decoration: none;
}

.add-card-btn {
  display: block;
  font-size: 1.4rem;
  font-weight: 400;
  color: #838c91;
  padding: 1rem;
  text-align: left;
  cursor: pointer;
}

.add-card-btn:hover {
  background-color: #cdd2d4;
  color: #4d4d4d;
  text-decoration: none;
}
</style>
