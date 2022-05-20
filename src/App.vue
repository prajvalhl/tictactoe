<template>
  <p>Hi Tic</p>
  <button @click="checkIsWinner">click</button>
</template>

<script>
import Icon from "./components/Icon.vue";
import Swal from "sweetalert2/dist/sweetalert2";

export default {
  name: "App",
  components: { Icon },
  data() {
    return {
      winMessage: "",
      isCross: true,
      itemArray: [],
      // itemArr: new Array(9).fill("empty"),
    };
  },
  watch: {
    winMessage: function (msg) {
      if (msg) {
        this.showDialog();
      }
    },
  },
  methods: {
    showDialog() {
      Swal.fire({
        icon: "info",
        title: "Game Over",
        text: `${this.winMessage}`,
      });
    },
    handleClick(itemNum) {
      if (this.winMessage) {
        return this.showDialog();
      }

      if (this.itemArray[itemNum]) {
        this.itemArray[itemNum] = this.isCross ? "cross" : "circle";
        this.isCross = !this.isCross;
      } else {
        return Swal.fire("Already filled");
      }

      this.checkIsWinner();
    },
    checkIsWinner() {
      if (
        this.itemArray[0] === this.itemArray[1] &&
        this.itemArray[0] === this.itemArray[2] &&
        this.itemArray[0]
      ) {
        this.winMessage = `${this.itemArray[0]} won`;
      } else if (
        this.itemArray[3] &&
        this.itemArray[3] === this.itemArray[4] &&
        this.itemArray[4] === this.itemArray[5]
      ) {
        this.winMessage = `${this.itemArray[3]} won`;
      } else if (
        this.itemArray[6] &&
        this.itemArray[6] === this.itemArray[7] &&
        this.itemArray[7] === this.itemArray[8]
      ) {
        this.winMessage = `${this.itemArray[6]} won`;
      } else if (
        this.itemArray[0] &&
        this.itemArray[0] === this.itemArray[3] &&
        this.itemArray[3] === this.itemArray[6]
      ) {
        this.winMessage = `${this.itemArray[0]} won`;
      } else if (
        this.itemArray[1] &&
        this.itemArray[1] === this.itemArray[4] &&
        this.itemArray[4] === this.itemArray[7]
      ) {
        this.winMessage = `${this.itemArray[1]} won`;
      } else if (
        this.itemArray[2] &&
        this.itemArray[2] === this.itemArray[5] &&
        this.itemArray[5] === this.itemArray[8]
      ) {
        this.winMessage = `${this.itemArray[2]} won`;
      } else if (
        this.itemArray[0] &&
        this.itemArray[0] === this.itemArray[4] &&
        this.itemArray[4] === this.itemArray[8]
      ) {
        this.winMessage = `${this.itemArray[0]} won`;
      } else if (
        this.itemArray[2] &&
        this.itemArray[2] === this.itemArray[4] &&
        this.itemArray[4] === this.itemArray[6]
      ) {
        this.winMessage = `${this.itemArray[2]} won`;
      }
    },
    reloadGame() {
      (this.winMsg = ""), (this.isCross = true), (this.itemArr = []);
    },
  },
};
</script>

<style>
main {
  height: 100vh;
}
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 5px;
}

.box {
  height: 150px;
}
</style>
