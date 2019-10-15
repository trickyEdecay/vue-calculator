<template>
  <div id="app">
      <div class="calculator-body">
          <div class="led">123123</div>
          <div class="btn-container">
            <div class="btn-top">
              <my-btn orange>AC</my-btn>
              <my-btn blue>/</my-btn>
              <my-btn blue>*</my-btn>
              <my-btn blue>-</my-btn>
            </div>
            <div class="btn-bottom">
              <div class="btn-left">
                <my-btn>7</my-btn>
                <my-btn>8</my-btn>
                <my-btn>9</my-btn>
                <my-btn>4</my-btn>
                <my-btn>5</my-btn>
                <my-btn>6</my-btn>
                <my-btn>1</my-btn>
                <my-btn>2</my-btn>
                <my-btn>3</my-btn>
                <my-btn wide>0</my-btn>
                <my-btn>.</my-btn>
              </div>
              <div class="btn-right">
                <my-btn blue long>+</my-btn>
                <my-btn orange long>=</my-btn>             
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
