<template>
  <transition-group name="pop">
    <div v-if="!isGameStarted && !timesUpVar" class="menu-main">
        <div class="gameTitle">
          <h1>
            INVOKER <br />
            SPELL SIMULATOR GAME
          </h1>
        </div>

        <div class="gameOptions">
          <h3 @click="startGame">Start Game</h3>
          <h3 @click="showTutorial">Tutorial</h3>
          <h3 @click="showAbout">About</h3>
        </div>
      </div>
  </transition-group>
</template>

<script>
export default {
  name: "mainMenu",

  props: [
    "startGame",
    "isGameStarted",
    "intervalTimer",
    "timesUpVar",
    "isShowAbout",
    "showAbout",
    "isShowTutorial",
    "showTutorial",
  ],

  data() {
    return {};
  },
};
</script>

<style lang="scss">

@import '@/assets/styles/scss/style.scss'

</style>