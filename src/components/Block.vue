<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
      Click Me
  </div>
</template>

<script>
export default {
    props: ['delay'],
    data(){
        return{
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },
    mounted(){
        setTimeout(()=>{
            this.showBlock = true
            this.startTimer()
        },this.delay)
    },
    methods:{
        startTimer(){
            //run every 10ms
            this.timer = setInterval(()=>{
                this.reactionTime +=10
            }, 10)
        },
        stopTimer(){
            //stop the function in startTimer to stop increasing reactionTime
            //and maintain user's reaction time in reactionTime
            clearInterval(this.timer)
            //send a custom event with the reactionTime
            this.$emit('end', this.reactionTime)
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