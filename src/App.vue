<template>
  <div class="topNav">
    <div class="logo">
      <h3>DevKobs</h3>
    </div>
    <div class="links"></div>
  </div>
  <!-- 
  <div class="sideNav">
    <div class="socialIcons">
      <a href="https://www.facebook.com/profile.php?id=61552791824063"
        ><img class="svg" src="@/assets/images/fb.png" alt=""
      /></a>
      <a href="https://github.com/Kobs03"
        ><img class="svg" src="@/assets/images/gh.png" alt=""
      /></a>
      <a href=""><img class="svg" src="@/assets/images/li.png" alt="" /></a>
    </div>
</div> -->

  <div class="main">
    <div class="container-main">
      <div class="infoArea">
        <div v-if="isGameStarted">
          <h3>SCORE &nbsp;: &nbsp; {{ score }}</h3>
        </div>
        <div v-else>
          <h3>current score &nbsp;: &nbsp; {{ currentScore }}</h3>
        </div>
        <b style="color: white"> | </b>
        <div v-if="isGameStarted">
          <h3>TIMER &nbsp;: &nbsp; {{ timer }}</h3>
        </div>
        <div v-else>
          <!-- kapag inideth mo tung high score mahina kang nilalang, payag ka ba non? -->
          <h3>highest score &nbsp;: &nbsp; {{ highestScore }}</h3>
        </div>
      </div>

      <!-- Game area -->
      <div class="container2">
        <div class="gameArea">
          <!-- glow mark-ups -->

          <transition name="popo">
            <div v-if="isMultiplierOn || rightInput != 0" class="glowArea">
              <div v-if="rightInput >= 5 || isMultiplierOn">
                <div class="innerCir"></div>
              </div>

              <div v-if="rightInput >= 10 || isMultiplierOn">
                <div class="outerCir"></div>
              </div>

              <div v-if="rightInput >= 15 || isMultiplierOn">
                <div class="glowBox"></div>
              </div>
            </div>
          </transition>

          <!-- orbit area -->

          <div class="orbit-container">
            <div class="orbit-outer">
              <div class="orbit-circle">
                <div :class="element[0].name"></div>
              </div>

              <div class="orbit-circle1">
                <div :class="element[1].name"></div>
              </div>

              <div class="orbit-circle2">
                <div :class="element[2].name"></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <spellDisplay
        :displaySpell="displaySpell"
        :generatedSpell="generateRandomSpell"
        :spellImg="spellImg"
        :quitGame="quitGame"
        :quitLogic="quitLogic"
      />
    </div>

    <div class="buttons">
      <button @click.prevent="quasButton">Quas</button>
      <button @click.prevent="wexButton">Wex</button>
      <button @click.prevent="exortButton">Exort</button>
      <button @click.prevent="castButton">Evoke</button>
    </div>

    <mainMenu
      :startGame="startGame"
      :isGameStarted="isGameStarted"
      :timesUpVar="timesUpVar"
      :isShowAbout="isShowAbout"
      :showAbout="showAbout"
      :showTutorial="showTutorial"
      :isShowTutorial="isShowTutorial"
    />

    <timesUp
      :startGame="startGame"
      :isGameStarted="isGameStarted"
      :timesUpVar="timesUpVar"
      :showTimesUp="showTimesUp"
      :currentScore="currentScore"
      :highestScore="highestScore"
      :score="score"
    />

    <about :isShowAbout="isShowAbout" :showAbout="showAbout" />

    <tutorial :showTutorial="showTutorial" :isShowTutorial="isShowTutorial" />
    
  </div>

  <footer>
    <div class="footerText">©2023 DevKobs, All rights reserved</div>
  </footer>
</template>


<script>
// gameplay algo flow
// start game button
// -> when clicked
// - countdown timer starts
// - set isGameStarted var to true
// - generate random spell object from data
// - wait for the user input
// - check if user input match the object data code
// - when true, score + 1
// - when timer runs out
// - set score to current score
// - if curr score > highest score
// - highest score = score
// - set isGameStarted var to false

import spellsData from "@/spells.json";
import mainMenu from "@/components/mainMenu.vue";
import timesUp from "@/components/timesUp.vue";
import spellDisplay from "@/components/spellDisplay.vue";
import about from "@/components/about.vue";
import tutorial from "@/components/tutorial.vue";

export default {
  name: "invokeGame",
  data() {
    return {
      element: ["quas", "wex", "exort"],
      elemIndex: 0,
      spellImg: "",
      displaySpell: [],
      message: "",
      toCompare: "",
      inputCount: -1,
      spells: spellsData, // spells data from locan json file
      generatedSpell: [], // expected data is single object from spells
      previousSpell: [],
      score: 0,
      timer: 0,
      isGameStarted: false,
      timesUpVar: false,
      highestScore: 0,
      currentScore: 0,

      // multiplier feature vars

      rightInput: 0,
      multiplierTimer: 10,
      isMultiplierOn: false,

      // menu vars
      isShowAbout: false,
      isShowTutorial: false,
    };
  },

  // components

  components: {
    mainMenu,
    timesUp,
    spellDisplay,
    about,
    tutorial,
  },

  methods: {
    //show About component

    showAbout() {
      this.isShowAbout = !this.isShowAbout;
    },

    //show tutorial component

    showTutorial() {
      this.isShowTutorial = !this.isShowTutorial;
    },

    //show times up component

    showTimesUp() {
      this.timesUpVar = !this.timesUpVar;
    },

    clickTest() {
      console.log("clicked mafakers!");
    },

    //generate random spells object

    generateRandomSpell() {
      let test = Math.floor(Math.random() * 10);
      // console.log(test);
      let result = this.spells[test];
      // console.log(result);
      this.generatedSpell = result;
    },

    // set interval logic || timer

    intervalTimer() {
      let test = setInterval(() => {
        this.timer--;
        // console.log(this.timer);
        if (this.timer <= 0) {
          clearInterval(test);
          this.isGameStarted = false;
          this.timesUpVar = true;
          this.currentScore = this.score;
          this.element = ["quas", "wex", "exort"];
          this.elemIndex = 0;
          if (this.currentScore > this.highestScore) {
            this.highestScore = this.currentScore;
          }
          this.score = 0;
          this.message = "";
          this.toCompare = "";
          this.generatedSpell = [];
          this.previousSpell = [];
          this.displaySpell = [];
          this.inputCount = -1;
          this.rightInput = 0;
          this.isMultiplierOn = false;
        }
      }, 1000);
    },

    // start game logic

    startGame() {
      this.timer = 60;
      this.isGameStarted = true;
      this.generateRandomSpell();
      this.displaySpell.push({
        image: this.generatedSpell.spellImg,
      });
      // console.log(this.generatedSpell.spellCodeArray);
      this.spellImg = this.generatedSpell.spellImg;
      this.isClicked = true;
      this.intervalTimer();
    },

    //quit game logic

    quitLogic() {
      this.isGameStarted = false;
      this.score = 0;
      this.message = "";
      this.toCompare = "";
      this.inputCount = -1;
      this.generatedSpell = [];
      this.previousSpell = [];
      this.timer = 0;
      this.currentScore = this.score;
      // this.highestScore = 0;
      this.element = ["quas", "wex", "exort"];
      this.elemIndex = 0;
      this.displaySpell = [];
      this.rightInput = 0;
      this.isMultiplierOn = false;
    },

    quitGame(e) {
      let keyCode = e.code;
      // console.log(keyCode);
      if (keyCode == "Escape") {
        this.isGameStarted = false;
        this.score = 0;
        this.message = "";
        this.toCompare = "";
        this.inputCount = -1;
        this.generatedSpell = [];
        this.previousSpell = [];
        this.timer = 0;
        this.currentScore = this.score;
        // this.highestScore = 0;
        this.element = ["quas", "wex", "exort"];
        this.elemIndex = 0;
        this.displaySpell = [];
        this.rightInput = 0;
        this.isMultiplierOn = false;
      }
    },

    // key inputs logic

    keyCodeLogic(str, elemClass) {
      if (this.isGameStarted) {
        this.element.push({ id: this.elemIndex, name: elemClass });
        if (this.element.length == 4) {
          this.element.splice(this.elemIndex, 1);
        }
        this.message += str;
        // console.log(this.message.length);
        this.toCompare = this.message;
        if (this.message.length >= 3) {
          this.inputCount++;
          // console.log(`input count: ${this.inputCount}`);
        }
        return this.toCompare;
      }
    },

    castLogic() {
      if (this.isGameStarted) {
        // console.log("key r pressed!");

        this.toCompare = this.toCompare.substring(this.inputCount);
        // console.log(`Spell cast : ${this.toCompare.toUpperCase()}`);

        if (this.generatedSpell.spellCodeArray.includes(this.toCompare)) {
          this.rightInput += 1;

          if (this.rightInput === 15) {
            this.isMultiplierOn = true;
            if (this.isMultiplierOn === true) {
              // console.log(this.score + " score multiplier active!");

              //multiplier timer On!

              let doubleScoreActive = setInterval(() => {
                this.multiplierTimer--;
                console.log(this.multiplierTimer);
                if (this.multiplierTimer === 0) {
                  clearInterval(doubleScoreActive);
                  this.isMultiplierOn = false;
                  this.multiplierTimer = 10;
                  this.rightInput = 0;
                  // console.log("score multiplier disabled!");
                }
              }, 1000);
            }
          }

          // console.log("rightInput Counter: " + this.rightInput);
          if (this.isMultiplierOn == false) {
            this.score += 1;
          } else if (this.isMultiplierOn == true) {
            this.score += 2;
          }

          this.previousSpell = this.generatedSpell;
          this.generateRandomSpell();
          // console.log(this.generatedSpell.spellCodeArray);
          this.spellImg = this.generatedSpell.spellImg;
          // console.log(
          //   " NEW GENERATED SPELL! " + this.generatedSpell.spellName
          // );
          if (this.previousSpell == this.generatedSpell) {
            // console.log("REPEATED SPELL");
            do {
              this.generateRandomSpell();
              // console.log(this.generatedSpell.spellCodeArray);
              this.spellImg = this.generatedSpell.spellImg;
            } while (this.previousSpell == this.generatedSpell);
            // console.log("REGENERATED SPELL " + this.generatedSpell.spellName);
            // this.generateRandomSpell();
            // console.log("REGENERATED SPELL "+this.generatedSpell.spellName)
          }
        } else {
          // console.log("wrong code!");
        }
      }
    },

    // keyboard input events

    quasKey(e) {
      let keyCode = e.code;
      if (keyCode == "KeyQ") {
        this.keyCodeLogic("q", "quas");
      }
    },

    wexKey(e) {
      let keyCode = e.code;
      if (keyCode == "KeyW") {
        this.keyCodeLogic("w", "wex");
      }
    },

    exortKey(e) {
      let keyCode = e.code;
      if (keyCode == "KeyE") {
        this.keyCodeLogic("e", "exort");
      }
    },

    //submit spell logic

    castKey(e) {
      let keyCode = e.code;
      if (keyCode == "KeyR") {
        this.castLogic();
      }
    },

    // mobile button inputs

    quasButton() {
      this.keyCodeLogic("q", "quas");
    },

    wexButton() {
      this.keyCodeLogic("w", "wex");
    },

    exortButton() {
      this.keyCodeLogic("e", "exort");
    },

    castButton() {
      this.castLogic();
    },
  },

  // event listeners

  created() {
    window.addEventListener("keypress", this.quasKey);
    window.addEventListener("keypress", this.wexKey);
    window.addEventListener("keypress", this.exortKey);
    window.addEventListener("keypress", this.castKey);
    window.addEventListener("keyup", this.quitGame);
  },
};
</script>

<style src="@/assets/styles/css/styles.css"></style>

