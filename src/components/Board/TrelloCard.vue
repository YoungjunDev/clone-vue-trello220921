<!--HTML-->
<template>
  <ul
    class="list-items"
    ref=" items"
    @drop.prevent="onDrop($event, idx)"
    @dragenter.prevent
    @dragover.prevent
  >
    <li
      v-for="(card, idx) in this.addTitle"
      v-bind:key="idx"
      draggable="true"
      @dragstart="startDrag($event, card)"
    >
      {{ card.card_title }}
    </li>
  </ul>
  <div class="list-card-labels" v-show="this.addOption.addCardDiv">
    <textarea
      name=""
      id="list-card-composer-textarea"
      cols="26"
      rows="10"
      placeholder=" Enter a title for this card..."
      v-model="newPutItem"
      v-on:keyup.enter="addTitle"
    ></textarea>
    <div class="list-update-col">
      <button class="add-card-update-btn" @click="addCardItem">Add card</button>
      <span class="add-list-close" @click="closeCard(item)">
        <i class="fa-solid fa-x"></i>
      </span>
    </div>
  </div>
  <button
    class="add-card-btn btn"
    @click="addCard()"
    v-show="this.addOption.addCardBtn"
  >
    &#43;Add a card
  </button>
</template>

<!--script-->
<script>
export default {
  props: ["card"],
  data() {
    return {
      addTitle: this.card.list_item,
      addOption: this.card.list_title,
      newPutItem: "", // input에서 받아오는 새 데이터용
    };
  },
  methods: {
    addCardItem() {
      const newdata = { card_detail: "", card_title: "" };
      if (this.newPutItem !== "") {
        newdata.card_title = this.newPutItem;
        this.addTitle.push(newdata);
        console.log(this.addTitle);
        this.clearInput();
      } else {
        console.log("실패");
      }
    },

    clearInput() {
      this.newPutItem = "";
      this.addOption.addCardDiv = !this.addOption.addCardDiv;
      this.addOption.addCardBtn = !this.addOption.addCardBtn;
    },

    addCard: function () {
      console.log(this.addOption.addCardDiv);
      this.addOption.addCardDiv = !this.addOption.addCardDiv;
      this.addOption.addCardBtn = !this.addOption.addCardBtn;
    },

    closeCard() {
      this.addOption.addCardDiv = !this.addOption.addCardDiv;
      this.addOption.addCardBtn = !this.addOption.addCardBtn;
    },

    startDrag(event, item) {
      event.dataTransfer.dropEffect = "move";
      event.dataTransfer.effectAllowed = "move";
      event.dataTransfer.setData("selectedItem", item.card_title);
    },

    // onDrop(event, idx) {
    //   const selectedItem = Number(event.dataTransfer.getData("selectedItem"));

    //   let targetIdx
    //   let targetItem

    //   this.
    // },
  },
};
</script>

<!-- css -->
<style scoped>
.list-items {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-content: start;
  padding: 0 0.6rem 0.5rem;
  overflow-y: auto;
  margin-bottom: 0.3rem;
}

.list-items::-webkit-scrollbar {
  width: 1.6rem;
}

.list-items::-webkit-scrollbar-thumb {
  background-color: #c4c9cc;
  border-right: 0.6rem solid #e2e4e6;
}

.list-items li {
  font-size: 1.4rem;
  font-weight: 400;
  line-height: 1.3;
  background-color: #fff;
  padding: 0.65rem 0.6rem;
  color: #4d4d4d;
  border-bottom: 0.1rem solid #ccc;
  border-radius: 0.3rem;
  margin-bottom: 0.6rem;
  word-wrap: break-word;
  cursor: pointer;
}

.list-items li:last-of-type {
  margin-bottom: 0;
}

.list-items li:hover {
  background-color: #eee;
}

.add-card-btn::after {
  content: "...";
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
