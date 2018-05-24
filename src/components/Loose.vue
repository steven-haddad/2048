<template>
    <div class="overlay" v-show="show">
        <p class="message">{{contents}}</p>
        <button class="tryAgain" @click="restart" >Try again</button>
    </div>
</template>

<script>
    export default{
        data(){
            return{
            }
        },
        props:{
            board:{
                type:Object,
                required:true
            },
            onrestart:{
                type:Function,
                required:true
            }
        },
        computed:{
            show(){
                this.Board.isOver()
            },
            contents(){
                if(this.Board.isOver()){
                    return 'GameOver!'
            
                }
            }
        },
        methods:{
            restart(){
                this.onrestart && this.onrestart()
            }
        },
        components:{
        }
    }
</script>