<template>
<section>
    <div class='timer'>
        <div class='timer__text'>
        <h1 class='timer__text__title'>One Minute Timer {{emojiIcon}} </h1>
        <span class='timer__text__seconds'>{{minutes}}:{{seconds}} <span><i>{{text}}</i></span></span>     
    </div>

    <div class='timer__button'>
        <button  v-if="!screenTime" @click="start">Start</button>
        <button  v-if="screenTime" @click="stop">Stop</button>
        <button  v-if="isReset" @click="reset">Reset</button>
    </div>
    </div>
    
</section>
</template>

<script>
import {ref,reactive} from "vue"
export default {
    data() {
        return {
            screenTime: null,
            emojiIcon: "⏰",
            totalTime: ref(1 * 60),
            isReset: true,
            text: ref('minute')

        }
    },
    methods:{
            start() {
                
                this.screenTime = setInterval(()=>this.timerCountdown(), 1000);
               
            
            },
            stop() {
                clearInterval(this.screenTime);
                this.screenTime = null;
               
            },
            reset() {
                clearInterval(this.screenTime);
                this.totalTime = (1 * 60);
                this.text = ref('minute')
                this.screenTime = null; 
                
            },
            editScreenTime(time) {
                return (time < 10 ? '0' : '') + time;  
            },
            timerCountdown() {
                this.totalTime--;
                if (this.totalTime == 0) {
                    this.reset()   
                }
                
                this.totalTime < 60 ? this.text = 'seconds' : ''
                this.totalTime >= 60 ? this.text = 'minute' : ''

            },
        },
         computed:{
            minutes() {
                return this.editScreenTime(Math.floor(this.totalTime / 60));
            },
            seconds() {
                return this.editScreenTime(this.totalTime - (this.minutes * 60));
            }
        }

}
</script>

<style lang="scss">


</style>