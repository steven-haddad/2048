<template>
    <div class="overlay">
        <button class="tryAgain" @click="restart" >Try again</button>
        <button class="saveGame" @click="saveGame" >Sauvegarder le score</button>
    </div>
</template>



<script>
export default {
  data() {
    return {};
  },
  methods: {
    restart() {
      this.$emit("restart");
    },
    saveGame() {
      this.$emit("saveGame");
    }
  },
  components: {}
};
</script>