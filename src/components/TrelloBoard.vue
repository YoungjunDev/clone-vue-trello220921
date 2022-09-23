<!--HTML-->
<template>
  <section class="board-container">
    <!-- {{ propsdata.board_item }} -->
    <List v-bind:board="propsdata.board_item" />
    <button
      class="add-list-btn btn"
      v-show="isHiddenBtn"
      v-on:click="openAddListContainer"
    >
      &#43;Add another list
    </button>
    <div class="list-container" v-show="isHiddenContainer">
      <div class="list-card-labels">
        <textarea
          name=""
          id="list-card-composer-textarea"
          cols="26"
          rows="10"
          placeholder=" Enter list title..."
          v-model="newlistItem"
          v-on:keyup.enter="addTitle"
        ></textarea>
        <div class="list-update-col">
          <button class="add-card-update-btn">Add card</button>
          <span class="add-list-close">
            <i class="fa-solid fa-x" v-on:click="closeAddListContainer"></i>
          </span>
        </div>
      </div>
    </div>
  </section>
</template>

<!--script-->
<script>
import List from "./Board/TrelloList.vue";

export default {
  name: "TrelloBoard",
  props: ["propsdata"],
  components: {
    List,
  },
  data() {
    return {
      isHiddenBtn: true,
      isHiddenContainer: false,
    };
  },
  methods: {
    openAddListContainer() {
      this.isHiddenBtn = !this.isHiddenBtn;
      this.isHiddenContainer = !this.isHiddenContainer;
    },
    closeAddListContainer() {
      this.isHiddenBtn = !this.isHiddenBtn;
      this.isHiddenContainer = !this.isHiddenContainer;
    },
  },
};
</script>

<!-- css -->
<style scoped>
.board-container::-webkit-scrollbar {
  height: 2.4rem;
}

.board-container::-webkit-scrollbar-thumb {
  background-color: #c4c4cc;
  border: 0.3rem solid #888888;
  border-top-width: 0;
}

.board-container {
  display: flex;
  align-items: start;
  padding: 0 0.8rem 0.8rem;
  overflow-x: auto;
  height: calc(100vh - 8.6rem);
}

.add-list-btn {
  flex: 0 0 27rem;
  display: block;
  font-size: 1.4rem;
  font-weight: 400;
  background-color: #495057;
  opacity: 0.3;
  color: #ffffff;
  padding: 1rem;
  border-radius: 0.3rem;
  cursor: pointer;
  transition: background-color 150ms;
  text-align: left;
  box-shadow: 0px 5px 5px #000000;
}

.add-list-btn:hover {
  background-color: #d3d3d3;
}

.add-list-btn::after {
  content: "...";
}

.list-container {
  flex: 0 0 27rem;
  display: flex;
  flex-direction: column;
  background-color: #e2e4e6;
  max-height: calc(100vh - 11.8rem);
  border-radius: 0.5rem;
  margin-right: 1rem;
  box-shadow: 0px 0px 10px #000000;
  padding-top: 0.8rem;
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
</style>
