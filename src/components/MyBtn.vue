<template>
  <div :class="['btn',{orange,blue,wide,long}]" @click="handleClick">
      <slot></slot>
  </div>
</template>

<script>
export default {
    name:"MyBtn",
    props:{
        orange:{
            type:Boolean,
            default:false
        },
        blue:{
            type:Boolean,
            default:false
        },
        wide:{
            type:Boolean,
            default:false
        },
        long:{
            type:Boolean,
            default:false
        }
    },
    methods:{
        handleClick(){
            this.$emit("click");
        }
    }
}
</script>

<style lang="less">
@btnSize: 60px;
@btnGap: 20px;
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