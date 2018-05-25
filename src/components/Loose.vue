<template>
    <div class="overlay">
        <button class="tryAgain" @click="restart" >Try again</button>
    </div>
</template>



<script>
export default {
  data() {
    return {}
  },
  methods: {
    restart() {
      this.$emit("restart")
    }
  },
  components: {}
};
</script>