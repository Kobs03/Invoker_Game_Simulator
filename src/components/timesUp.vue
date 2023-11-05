<template>
  <transition-group name="pop">
    <div @click="showTimesUp" v-if="timesUpVar" class="main-timesUp">
      <div>
        <h1 v-if="timesUpVar && currentScore != 0">Times Up !</h1>
        <h1 v-else-if="currentScore == 0">Thanks For Playing !</h1>
      </div>
      <div class="scoreDisplay">
        <h2 v-if="currentScore === 0"></h2>
        <h2 v-else-if="currentScore < highestScore">
          Score : {{ currentScore }}
        </h2>
        <h2 v-else>New High Score : {{ highestScore }}</h2>
        <br />
        <p style="color: white; text-shadow: 0 0 10px #FF3131;">Click anywhere to continue</p>
      </div>

      <img
        v-if="currentScore === 0"
        class="puckYou"
        src="@/assets/images/puckYou.png"
        alt=""
      />

      <img
        v-else-if="currentScore < highestScore"
        class="rylai"
        src="@/assets/images/cm.png"
        alt=""
      />
      <img v-else class="invoPNG" src="@/assets/images/invoChibi.png" alt="" />
    </div>
  </transition-group>
</template>

<script>
export default {
  name: "mainMenu",

  props: [
    "startGame",
    "isGameStarted",
    "timesUpVar",
    "score",
    "currentScore",
    "highestScore",
    "showTimesUp",
  ],

  data() {
    return {};
  },
};
</script>

<style src="@/assets/styles/css/styles.css"></style>