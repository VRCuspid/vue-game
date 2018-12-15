<template>
  <div class="gamebox">
    <ul class="square">
      <li v-for="(item,i) in arr" :key="i" v-if="item==0" class="none"></li>
      <li v-else @click="move(i)">{{reN(i)}}</li>
    <button class="reset" @click="resetGame">重置游戏</button>
    <button class="success" @click="success">一键还原</button>
    </ul>
  </div>
</template>
<script>
export default {
  name:'gameBox',
  data(){
    return {
      active:15,
      arr:Array.from({length:15}).fill(0).map(function(item,i){return i+1}).sort(function(a,b){return 0.5-Math.random()}).concat([0])
    }
  },
  mounted(){
    console.log(this.arr);
  },
  methods:{
    success(){
      this.active=15;
      this.arr=Array.from({length:15}).fill(0).map(function(item,i){return i+1}).concat([0]);
    },
    reN(i){
      return this.arr[i];
    },
    resetGame(){
      this.arr=Array.from({length:15}).fill(0).map(function(item,i){return i+1}).sort(function(a,b){return 0.5-Math.random()}).concat([0]);
      this.active=15;
    },
    move(i){
      if(i==this.active-1||i==this.active+1||i==this.active-4||i==this.active+4){
        this.arr[this.active]=this.arr[i];
        this.$set(this.arr,i,0)
        this.active=i;
      }
    }
  }
}
</script>
<style lang="scss" scoped>
ul,li{
  list-style: none;
}
.square{
  margin:10px;
   margin:0;
  width:200px;
  font-size: 0;
  li{
    font-size:20px;
    display:inline-block;
    width:25%;
    height:50px;
    border:1px solid #ccc;
    text-align: center;
    line-height: 50px;
    box-sizing: border-box;
    background:#f90;
    color:#fff;
    overflow: hidden;
    transition:1s;
    margin:0;
  }
  .reset,.success{
    width:80%;
    height:30px;
    border:0;
    outline: 0;
    background: #f90;
    border-radius: 10px;
    text-align: center;
    line-height: 30px;
    color:#fff;
    margin-top:10px;
  }
  .none{
    background:#ccc;
    box-shadow: 0 0 10px #000 inset;
  }
}
</style>


