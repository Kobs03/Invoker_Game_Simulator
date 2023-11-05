<template>
  <div v-for="spells of displaySpell" :key="spells.id" class="spellImg">
    <img
      @click="quitLogic"
      v-if="displaySpell.length"
      :class="spells.spellImg"
      :src="spellImg"
      alt=""
    />
  </div>
</template>

<script>
export default {
  props: ["displaySpell", "generatedSpell", "spellImg","quitGame","quitLogic"],
};
</script>

<style src="@/assets/styles/css/styles.css"></style>