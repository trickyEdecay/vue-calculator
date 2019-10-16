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
  computed:{
    led(){
      if(this.errorText!==""){
        return this.errorText;
      }
      if(this.isNewRound){
        return this.result;
      }
      if(this.isInputingNumTwo && !this.isInputingNumOne){
        return parseFloat(this.numTwo);
      }else{
        return parseFloat(this.numOne);
      }
    },
  },
  data(){
    return {
      
      numOne:"0",
      numTwo:"0",
      result:"0",
      operator:"",
      // 是否正在输入第二个数
      isInputingNumTwo:false,
      // 是否正在输入第一个数字
      isInputingNumOne:true,
      // 是否是新的回合
      isNewRound:false,
      // 错误文本
      errorText:"",
    }
  },
  methods:{
    // 点击按钮和小数点
    pressNumber(num){
      if(this.isNewRound){
        this.numOne = "0";
      }
      this.isNewRound = false;
      if(!this.isInputingNumTwo){
        if(num === "." && this.numOne.indexOf('.')>=0){
          return;
        }
        this.numOne = this.numOne + num + "";
        return;
      }
      this.isInputingNumOne = false;
      if(num === "." && this.numTwo.indexOf('.')>=0){
        return;
      }
      this.numTwo = this.numTwo + num + "";
    },
    // 清空
    allclear(){
      this.numOne = "0";
      this.numTwo = "0";
      this.result = "0";
      this.isInputingNumTwo = false;
      this.isNewRound = true;
      this.isInputingNumOne = true;
      this.errorText = "";
    },
    // 点击操作符
    pressOperator(ope){
      this.operator = ope;
      this.isInputingNumTwo = true;
      this.numTwo = "0";
    },
    // 点击等于号
    equalHandler(){
      this.numOne = parseFloat(this.numOne);
      this.numTwo = parseFloat(this.numTwo);
      switch(this.operator){
        case "+":
          this.result = parseFloat((this.numOne+this.numTwo).toPrecision(12))+"";
          break;
        case "-":
          this.result = parseFloat((this.numOne-this.numTwo).toPrecision(12))+"";
          break;
        case "*":
          this.result = parseFloat((this.numOne*this.numTwo).toPrecision(12))+"";
          break;
        case "/":
          if(this.numTwo===0){
            this.errorText = "除数不能为0";
          }
          this.result = parseFloat((this.numOne/this.numTwo).toPrecision(12))+"";
          break;
      }
      this.numOne = this.result;
      this.isNewRound = true;
      this.isInputingNumOne = true;
      this.isInputingNumTwo = false;
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
