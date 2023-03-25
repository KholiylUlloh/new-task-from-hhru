<template>
  <div class="stopwatch_wrap">
    <Timer v-for="i in count" />
    <div class="add_btn">
      <img @click="addNew" width="20" src="./assets/plus.svg" alt="plus" />
    </div>
  </div>
</template>

<script>
import Timer from "./components/timer/timer.vue";
export default {
  components: {
    Timer,
  },
  data() {
    return {
      count: 1,
    };
  },
  methods: {
    addNew() {
      this.count++;
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.stopwatch_wrap {
  background: #353638;
  width: 100%;
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(auto-fill, 225px);
  grid-template-rows: repeat(auto-fill, 120px);
  padding: 72px 59px;
  align-items: center;
  justify-content: center;
  gap: 50px;
  grid-row-gap: 45px;
  overflow-y: scroll;
}
.add_btn {
  width: 225px;
  height: 120px;
  background-color: #696969;
  display: flex;
  align-items: center;
  justify-content: center;
}
@font-face {
  font-family: "Gotham Pro";
  src: url(./assets/gothampro_light.ttf);
}

@media screen and(max-width: 1024px) {
  .stopwatch_wrap {
    padding: 72px 212px;
  }
}
@media screen and(max-width: 768px) {
  .stopwatch_wrap {
    padding: 72px 135px;
  }
}
@media screen and(max-width: 400px) {
  .stopwatch_wrap {
    padding: 72px 0px;
  }
}
</style>
