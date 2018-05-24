<template>
    <div class="overlay">
        <button class="tryAgain" @click="restart" >Try again</button>
    </div>
</template>



<script>
import game from "@/components/Game.vue";


    export default{
        data(){
            return{
            }
        },
        methods:{
            restart(){
                this.$emit('retry')
              game.initBoard();
              
              
            }
        },
        components:{
        }
    }
</script>