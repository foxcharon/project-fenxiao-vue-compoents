<template>   
	<div class="card-gift">
    <div class="top">
      <div><slot name="row1-1"></slot></div>
      <div><slot name="row1-2"></slot></div>
    </div>
    <div class="center">
      <slot name="row2"></slot>
    </div>
	  <div class="bottom">      
      <slot name="row3"></slot>
    </div>    
	</div>
</template>

<script>
export default {
	name: 'CardGift',
    componentName: 'CardGift',

    data() {
      return {
        
      }
    },
 	  props: {    
      gray: {
        type: Boolean,
        default: false
      },
      bold: {
        type: Boolean,
        default: false
      },
      red: {
        type: Boolean,
        default: false
      },
      type:{
        type: Number,
        default: 1
      },
      boldLeft: {
        type: Boolean,
        default: false
      },
 	  }
 	
}
</script>

<style lang="less" scoped> 
@fs12:3.2vw;
@fs14:3.733vw;
@fs15:4vw;
@fs16:4.267vw;
@fs17:4.533vw;
@fs20:5.333vw;
@fs22:5.867vw;

@pd1:2.666vw;
@pd2:3.333vw;
@bw:100vw;
@bh:23.333vw;
@iw:16.666vw;
@gray:#bfc0c0;
@gray2:#666464;
@black1:#333232;
@red:#fd5265;

body,p,h1,h2,h3,h4,h5,h6,img{
	padding: 0;
	margin:0;
	border:0;
}
  
  .card-gift{
    min-height: 13.4375rem;
    background: #fff;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    .top,.center,.bottom{
      padding: 0 0.625rem;
    }
    .top,.bottom{
      display: flex;
      justify-content: space-between;   
      height: 3.125rem;
      line-height: 3.125rem;
    }
    .top{      
      font-size: @fs16;
      color: #fff;
      background: @red;
        
    }
    .center{
      min-height: 7.1875rem;
      font-size: @fs14;
      padding: 0.125rem 0.625rem 0.125rem;
      line-height: 2;
      border-bottom: 1px solid #e5e5e5;
      word-break: break-all;
    }
    .bottom{
      height: 3.125rem;
      line-height: 3.125rem;      
      font-weight: 700;
      font-size: @fs14;
      div{        
        height: 3.125rem;
        line-height: 3.125rem;
        &.buy{
          font-size: @fs16;
          span{
            width: @fs14;
            height: @fs14;
            margin-right: @fs14 / 2;
            vertical-align: -2.5%;
            display: inline-block;
            background-image: url("../../assets/images/new/gifts_001.png");
            background-repeat: no-repeat;
            background-size: 100%;
            &.active{
              background-image: url("../../assets/images/new/gifts_002.png");
            }
          }
        }    
        div:last-child{
          display:inline-block;
          width: 0.40625rem;
          height: 0.625rem;
          background-image: url("../../assets/images/new/ordersubmit_001.png");
          background-repeat: no-repeat;
          background-size: 100%;
        }
      }      
    }
  }
</style>


