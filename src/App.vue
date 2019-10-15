<template>
  <div id="app">
      <div class="calculator-body">
          <div class="led">123123</div>
          <div class="btn-container">
            <div class="btn-top">
              <div class="btn orange">AC</div>
              <div class="btn blue">/</div>
              <div class="btn blue">*</div>
              <div class="btn blue">-</div>
            </div>
            <div class="btn-bottom">
              <div class="btn-left">
                <div class="btn">7</div>
                <div class="btn">8</div>
                <div class="btn">9</div>
                <div class="btn">4</div>
                <div class="btn">5</div>
                <div class="btn">6</div>
                <div class="btn">1</div>
                <div class="btn">2</div>
                <div class="btn">3</div>
                <div class="btn wide">0</div>
                <div class="btn">.</div>
              </div>
              <div class="btn-right">
                <div class="btn long blue">+</div>
                <div class="btn long orange">=</div>                
              </div>
            </div>
          </div>
      </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  components: {
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
.btn{
  transition:all .2s;
  flex-shrink: 0;
  width:@btnSize;
  height:@btnSize;
  background:white;
  color:#333;
  border:1px solid #e5e5e5;
  box-sizing: border-box;
  font-family: sans-serif;
  font-weight: bold;
  font-size:16px;
  margin-right:@btnGap;
  margin-bottom: @btnGap;
  border-radius:10px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  user-select: none;

  &:hover{
    background:darken(#fff,10%);
  }

  &.wide{
    width:@btnSize*2+@btnGap;
  }

  &.long{
    height:@btnSize*2+@btnGap;
  }

  &.orange{
    background:#ee8a54;
    color:#fff;
    border:0;

    &:hover{
      background:darken(#ee8a54,10%);
    }
  }

  &.blue{
    background:#519aec;
    color:#fff;
    border:0;

    &:hover{
      background:darken(#519aec,10%);
    }
  }
}
</style>
