<template>
  <transition-group name="pop">
    <div v-if="isShowAbout" class="aboutMain">
      <div class="aboutContents">
        <p>
          <span>Invoker Spell Simulator v.01</span>
          <br />
          Created by: DevKobs <br />
          <br />
          Do you see this project fancy? <br />
          Please do follow me on my social account <br />
          and a GitHub star on this project. <br />
          <br />
          <span>links:</span> <br />
          <a href=""> Facebook Page </a> <br />
          <a href=""> Give this project a star </a> <br />
          <br />
          <span>Disclaimer:</span> <br />
          Image assets used in this game is not mine <br />
          and deserves a rightful credits to the owners.
        </p>
      </div>

      <div class="close" @click="showAbout">
        <p>close</p>
      </div>

    </div>
  </transition-group>
</template>
  
  <script>
export default {
  name: "aboutMenu",

  props: ["isGameStarted", "isShowAbout", "showAbout"],

  methods: {
    clickTest() {
      console.log("clicked!");
    },
  },
};
</script>
  
<style lang="scss">
@import "@/assets/styles/scss/style.scss";
</style>