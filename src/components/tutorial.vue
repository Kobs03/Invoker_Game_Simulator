<template>
  <transition-group name="pop">
    <div v-if="isShowTutorial" class="tutorial-main">

      <h3 id="control">Controls</h3>

      <div class="inputsCategory">
        <div class="kb">
          <div>keyboard</div>
        </div>
        <div class="mb">
          <div>Mobile</div>
        </div>
      </div>

      <div class="inputs-container">
        <div class="keyboard">
          <div class="keyQ">
            <div class="code1"><h3>Q</h3></div>
            <div class="arrow">=></div>
            <div class="ball1"></div>
          </div>
          <div class="keyW">
            <div class="code2"><h3>W</h3></div>
            <div class="arrow">=></div>
            <div class="ball2"></div>
          </div>
          <div class="keyE">
            <div class="code3"><h3>E</h3></div>
            <div class="arrow">=></div>
            <div class="ball3"></div>
          </div>
          <div class="keyR">
            <div class="code4"><h3>R</h3></div>
            <div class="arrow">=></div>
            <div class="ball4">Cast</div>
          </div>
        </div>

        <div class="mobile">
          <div class="mobileQ">
            <div class="touch1"><h5>Quas</h5></div>
            <div class="arrow">=></div>
            <div class="mobileBall1"></div>
          </div>
          <div class="mobileW">
            <div class="touch2"><h5>Wex</h5></div>
            <div class="arrow">=></div>
            <div class="mobileBall2"></div>
          </div>
          <div class="mobileE">
            <div class="touch3"><h5>Exort</h5></div>
            <div class="arrow">=></div>
            <div class="mobileBall3"></div>
          </div>
          <div class="mobileR">
            <div class="touch4"><h5>Evoke</h5></div>
            <div class="arrow">=></div>
            <div class="mobileBall4">Cast</div>
          </div>
        </div>
      </div>

      <div class="instructions-container">
        <p>
          <span> Instructions : </span>
          Input the right element combination of the displayed spell to gain
          points within 60 seconds. For every 15 right combination inputs,
          doubles the points gained for 10 seconds.
          <br />
        </p>
        <span @click="showTutorial" class="close"> Close </span>
      </div>
    </div>
  </transition-group>
</template>
    
    <script>
export default {
  name: "tutorialMenu",

  props: ["isShowTutorial", "showTutorial"],

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