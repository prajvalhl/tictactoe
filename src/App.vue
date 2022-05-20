<template>
  <main
    class="d-flex flex-column justify-content-center align-items-center bg-dark"
  >
    <div class="container">
      <div class="row justify-content-center mt-3">
        <div class="col col-6">
          <div class="text-center">
            <div v-if="!winMessage">
              <h1 class="text-info" v-show="isCross">Cross's Turn</h1>
              <h1 class="text-info" v-show="!isCross">Circle's Turn</h1>
            </div>
            <div v-else>
              <h1 class="text-warning">{{ winMessage.toUpperCase() }}</h1>
            </div>
          </div>
          <div class="grid">
            <div
              v-for="(item, i) in itemArr"
              @click="handleClick(i)"
              :key="i"
              class="card card-body box justify-content-center align-items-center bg-light"
            >
              <Icon :iconName="'empty'"></Icon>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import Icon from "./components/Icon-comp.vue";
import Swal from "sweetalert2/dist/sweetalert2";

export default {
  name: "App",
  components: { Icon },
  data() {
    return {
      winMessage: "",
      isCross: true,
      itemArr: new Array(9).fill("empty"),
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
        console.log(this.isCross);
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
