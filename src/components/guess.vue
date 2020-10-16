<template>
    <div><input v-model="input" type=text></div>
    <button @click="guess">Start</button>

</template>



<script>
export default {
    data(){
        return{
            input:''
        }
    },
    methods:{
        guess(){
            let random = Math.floor(Math.random()*100);
            let ans = "";
            if(ans == random){
                console.log('Done')
            }
        }
    }
}
</script>