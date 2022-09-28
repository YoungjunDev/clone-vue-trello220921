<!--HTML-->
<template>
  <div
    class="list"
    v-for="(item, idx) in this.updateTitle"
    v-bind:key="idx"
    draggable="true"
  >
    <div class="title-menu">
      <!-- {{ board }} -->
      <span>
        <h3
          class="list-title"
          v-show="item.list_title.titleChangeh3"
          @click="openTitle(item)"
        >
          {{ item.list_title.listTitle }}
        </h3>
      </span>
      <input
        class="list-title-input"
        v-show="item.list_title.titleChangeInput"
        v-model="item.list_title.listTitle"
        @blur="closeTitle(item)"
      />
      <button class="action-menu">
        <i class="fa-solid fa-ellipsis"></i>
      </button>
    </div>
    <Card v-bind:card="item" />
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
      updateTitle: this.board,
    };
  },
  methods: {
    openTitle: function (item) {
      // console.log(item.list_title.listTitle);
      item.list_title.titleChangeh3 = !item.list_title.titleChangeh3;
      item.list_title.titleChangeInput = !item.list_title.titleChangeInput;
    },

    closeTitle: function (item) {
      item.list_title.titleChangeh3 = !item.list_title.titleChangeh3;
      item.list_title.titleChangeInput = !item.list_title.titleChangeInput;
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
</style>
