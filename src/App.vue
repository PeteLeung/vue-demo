<template>
  <div class="wrapper">
    <div>第{{n}}步</div>
    <div class="">
      <div class="row">
        <Cell @click="onClickCell(0,$event)" :n="n" :finished="finished"/>
        <Cell @click="onClickCell(1,$event)" :n="n"  :finished="finished"/>
        <Cell @click="onClickCell(2,$event)" :n="n"  :finished="finished"/>
      </div>
      <div class="row" >
        <Cell @click="onClickCell(3,$event)" :n="n"  :finished="finished"/>
        <Cell @click="onClickCell(4,$event)" :n="n"  :finished="finished"/>
        <Cell @click="onClickCell(5,$event)" :n="n"  :finished="finished"/>
      </div>
      <div class="row">
        <Cell @click="onClickCell(6,$event)" :n="n"  :finished="finished"/>
        <Cell @click="onClickCell(7,$event)" :n="n"  :finished="finished"/>
        <Cell @click="onClickCell(8,$event)" :n="n"  :finished="finished"/>
      </div>
    </div>
    <div>{{map}}</div>
    <div>
      <button class="button" @click="reload">重置</button>
      结果：{{result === null ? '比赛中':`胜方为${result}`}}
    </div>
  </div>
</template>

<script>
import Cell from './Cell'
export default {
  components: {
    Cell
  },
  data(){
    return{
      finished:false,
      n:0,
      map:[[null,null,null],[null,null,null],[null,null,null]],
      result:null
    }
  },
  methods:{
    onClickCell(i,text){
      console.log(`${i}号格子被点击，内容:${text}`);
      this.map[Math.floor(i/3)][i%3] = text;
      this.n += 1;
      this.bingo();
    },
    bingo(){
      const map = this.map;
      for(let i=0;i<=2;i++){
        if(map[i][0]!=null&&map[i][0]===map[i][1]&&map[i][1]===map[i][2]){
            this.result = map[i][0];
            this.finished = true;
        }
        if(map[0][i]!=null&&map[0][i]===map[1][i]&&map[1][i]===map[2][i]){
            this.result = map[0][i];
            this.finished = true;
        }
        if(map[0][0]!=null&&map[0][0]===map[1][1]&&map[1][1]===map[2][2]){
            this.result = map[0][0];
            this.finished = true;
        }
        if(map[0][2]!=null&&map[0][2]===map[1][1]&&map[1][1]===map[2][0]){
            this.result = map[0][2];
            this.finished = true;
        }    
      }
    },
    reload(){
      window.location.reload();
    }
  }
};
</script>

<style>
.row{
  display: flex;
}
.wrapper{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.button{
  margin-right: 60px;
}
</style>
