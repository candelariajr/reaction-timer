<template>
  <div class="block" v-if="showBlock" @click="stopTimer">Click Me</div>
</template>

<script>
export default {
  name: "Block",
  props: ['delay'],
  mounted(){
    //on loading this component start the timer for the length of time specified in the delay prop
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay)
  },data(){
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0
    }
  }, methods:{
    //store the timer interval as an object
    startTimer(){
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10)
    },
    //remove the timer instance, fire event to indicate that game is no longer being played
    stopTimer(){
      clearInterval(this.timer);
      console.log(this.reactionTime);
      this.$emit('end', this.reactionTime);
    }
  }
}
</script>

<style>
  .block{
    width: 400px;
    border-radius: 20px;
    background: #0faf87;
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
  }
</style>