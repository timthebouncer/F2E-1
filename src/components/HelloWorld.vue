<template>
    <div class="container">
        <el-container>

            <el-container>
                <div class="aside">
                    <el-aside style="width: 70%">
                        <div class="add" style="width: 450px">
                            <input v-model="input" type="text" placeholder="add a new mission" style="border: 0px" />
                            <el-button @click="newThing" icon="el-icon-plus"></el-button>
                        </div>
                        <div class="clock">
                            <div></div>
                        </div>
                        <div class="playing">
                            <div class="control">
                                <span>{{doing}}</span>
                            </div>
                            <div class="playingTimer">
                                {{displayMinutes}}:{{displaySeconds}}</div>
                        </div >

                            <ul class="listGroup" style="z-index: 2;" v-for="(item) in list">
                                <li class="listGroup-item">
                                    <div class="customControl">
                                        <input type="checkbox"/>
                                        {{item}}
                                    </div>
                                    <el-button @click="portalHandle(item)" icon="el-icon-video-play"></el-button>
                                </li>
                            </ul>

                    </el-aside>
                    <div class="countDown" style="z-index:100">
                        <div class="start" @click="countDown"></div>
                    </div>
                </div>

                <div class="main">
                    <div class="iconAdjust">
                        <div @click="showHandle"><i class="el-icon-s-unfold"></i></div>
                        <div><i class="el-icon-s-data"></i></div>
                        <div><i class="el-icon-headset"></i></div>
                        <div><i class="el-icon-refresh"></i></div>
                    </div>
                </div>

            </el-container>
        </el-container>
    </div>
</template>

<script>
  export default {
      data(){
          return{
              totalSeconds:25 * 60,
              timer: null,
              started:false,
              down:'',
              temp:'',
              input:'',
              edit:'',
              list:["吃飯","睡覺"],
              doing:""
          }
      },

          // this.updateTime()
          // this.timer = setInterval(() => {
          //     // console.log(123)
          //     this.updateTime()
          // }, 1000)
      computed:{
            dataTypeChange: function () {
                return this.time / 1000
            },
          displayMinutes(){
                const minutes = Math.floor(this.totalSeconds / 60)
                return this.formatTime(minutes)
          },
          displaySeconds(){
              const seconds = this.totalSeconds % 60
              return this.formatTime(seconds)
          }
      },
      methods:{
          formatTime(time){
              if(time < 10){
                  return '0' +time
              }
              return time.toString()
          },
          countDown(){
              const vm = this

              if(vm.started === false){
                  vm.started = true
                  vm.timer=setInterval(function () {
                      if(vm.time <= 0){
                          return clearInterval(vm.timer)
                      }
                      vm.totalSeconds -= 1
                  }, 1000)
              }else{
                  this.started = false
                  this.stop()
              }
          },
          stop(){
              clearInterval(this.timer)
          },
          newThing(){
              if(this.input){
                  this.list.push(this.input)
              }
              this.input=""
          },
          portalHandle(item){
              this.doing = item
          },
          showHandle(){
              alert(0.0)
          }
      }
  }
</script>
<style>
    body{
        margin:0;
        background-color: #777;
        font-family: 'Roboto', sans-serif;
    }
    .container{
        width: 100%;
        padding-right: 15px;
        padding-left: 15px;
        margin-right: auto;
        margin-left: auto;
    }
    .el-container{
        margin-right: -15px;
        margin-left: -15px;
    }
    .add{
        margin-top: 20px;
        margin-left: 20px;
        display: flex;
        justify-content: space-between;
        padding: 1rem;
        background-color: #fff;
    }
    .aside{
        background-color: #ffedf7;
        position: relative;
        padding-left: 15px;
        width: 70%;
    }
    .el-aside{
        width: 50%;
        height: 100vh;
        padding: 3rem;
    }
    .main{
        width: 30%;
        /*flex:initial;*/
        background-color: #003164;
    }
    .clock{
        margin-top: 20px;
        position: relative;
    }
    .control{
        display: flex;
        height: 100px;
        width: 100px;
        padding-left: 4rem;
        font-size: 1.5rem;
        justify-content: space-between;

    }
    .playing{
    margin-top: 50px;
    }
    .playingTimer{
        position: relative;
        top: -50px;
        color: #ff4384;
        font-size: 11rem;
    }
    .listGroup{
        position: relative;
        top:250px;
        padding-left: 0;
        margin-bottom: 0;
    }
    .listGroup-item{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        position: relative;
    }
    ul {
        list-style: none;
        border-bottom: 1px solid #a4da89;
        width: 550px;
    }
    .countDown{
        position: absolute;
        top: 0;
        right: 0;
        transform: translate(50%,15%);
        width: 730px;
        height: 730px;
        background-color: #FF4384;
        border-radius: 50%;
    }
    .iconAdjust{
        display: flex;
        flex-direction: column;
        align-items: flex-end;
        width: 90%;
        height: 90%;
        color: #00ffff;
    }
    .iconAdjust >div:first-child{
        margin-top: 30px;
    }
    .iconAdjust >div{
        font-size: xx-large;
        margin-bottom: 30px;
        margin-right: 50px;;
    }
    .iconAdjust >div:hover{
        margin-bottom: 10px;
        font-size: xxx-large;
    }
    .start{
        position: absolute;
        top: 50px;
        right: 50px;
        transform: translate(-235%,225%);
        width: 110px;
        height: 110px;
        background-color: #00ffff;
        border-radius: 50%;
        background-image:url("https://image.shutterstock.com/image-vector/line-play-button-icon-illustration-260nw-1044448477.jpg");
        background-size: cover;
    }
    .start:hover{
        position: absolute;
        top: 50px;
        right: 50px;
        transform: translate(-160%,145%);
        /*transition: all 1.5s;*/
        width: 150px;
        height: 150px;
        background-color: #00ffff;
        border-radius: 50%;
    }

</style>