<template>
  <div id="app">
      <div class="calculator-body">
          <div class="led">{{led}}</div>
          <div class="btn-container">
            <div class="btn-top">
              <my-btn orange @click="allclear">AC</my-btn>
              <my-btn blue @click="pressOperator('/')">/</my-btn>
              <my-btn blue @click="pressOperator('*')">*</my-btn>
              <my-btn blue @click="pressOperator('-')">-</my-btn>
            </div>
            <div class="btn-bottom">
              <div class="btn-left">
                <my-btn @click="pressNumber(7)">7</my-btn>
                <my-btn @click="pressNumber(8)">8</my-btn>
                <my-btn @click="pressNumber(9)">9</my-btn>
                <my-btn @click="pressNumber(4)">4</my-btn>
                <my-btn @click="pressNumber(5)">5</my-btn>
                <my-btn @click="pressNumber(6)">6</my-btn>
                <my-btn @click="pressNumber(1)">1</my-btn>
                <my-btn @click="pressNumber(2)">2</my-btn>
                <my-btn @click="pressNumber(3)">3</my-btn>
                <my-btn wide @click="pressNumber(0)">0</my-btn>
                <my-btn @click="pressNumber('.')">.</my-btn>
              </div>
              <div class="btn-right">
                <my-btn blue long @click="pressOperator('+')">+</my-btn>
                <my-btn orange long @click="equalHandler">=</my-btn>             
              </div>
            </div>
          </div>
      </div>
  </div>
</template>

<script>
import MyBtn from './components/MyBtn'
export default {
  name: 'app',
  components: {
    MyBtn
  },
  data(){
    return {
      led:"",
      numOne:0,
      numTwo:0,
      result:0,
      operator:"",
      isInputingNumTwo:false,
      isNewRound:false,
      // 是否拥有小数点
      hasDecimalPoint:false,
    }
  },
  methods:{
    pressNumber(num){
      // 处理小数点
      if(num === "."){
        if(this.hasDecimalPoint){
          return;
        }
        this.led = this.led+ ".";
        this.hasDecimalPoint = true;
        return;
      }
      // 处理数字
      if(this.operator==="" || this.isInputingNumTwo){
          if(this.isNewRound){
            this.led = num+"";
            this.isNewRound = false;
            return;
          }
          this.led = this.led+num;
          return;
      }
      this.led = num+"";
      this.isInputingNumTwo = true;
    },
    allclear(){
      this.led = "";
    },
    pressOperator(ope){
      this.numOne = parseFloat(this.led);
      this.operator = ope;
      this.hasDecimalPoint = false;
    },
    equalHandler(){
      this.numTwo = parseFloat(this.led);
      switch(this.operator){
        case "+":
          this.led = parseFloat((this.numOne+this.numTwo).toPrecision(12))+"";
          break;
        case "-":
          this.led = parseFloat((this.numOne-this.numTwo).toPrecision(12))+"";
          break;
        case "*":
          this.led = parseFloat((this.numOne*this.numTwo).toPrecision(12))+"";
          break;
        case "/":
          this.led = parseFloat((this.numOne/this.numTwo).toPrecision(12))+"";
          break;
      }
      this.operator = "";
      this.numOne = 0;
      this.numTwo = 0;
      this.isNewRound = true;
      this.isInputingNumTwo = false;
      this.hasDecimalPoint = false;
    }
  }
}
</script>

<style lang="less">
html,body{
  background:#e5e5e5;
  margin:0;
}
@btnSize: 60px;
@btnGap: 20px;
.calculator-body{
  width:@btnSize*4+@btnGap*3;
  height:@btnSize*6+@btnGap*5;
  margin:0 auto;
  margin-top: 60px;
  background:#fff;
  border-radius: 10px;
  padding:40px;
}

.led{
  width:100%;
  height:@btnSize;
  background:#dadada;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  font-size:20px;
  padding: 0 10px;
  box-sizing: border-box;
  border-radius: 10px;
  margin-bottom:@btnGap;
}

.btn-top{
  display: flex;

  .btn:last-of-type{
    margin-right:0;
  }
}
.btn-bottom{
  display: flex;
}
.btn-left{
  display: flex;
  flex-wrap: wrap;
}
.btn-right{
  .btn{
    margin-right:0;
  }
}
</style>
