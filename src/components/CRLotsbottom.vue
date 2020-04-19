<template>
<div>
  <div class="pic-box" v-if="linetype === 1">
    <slot></slot>
    
  </div>
  <div class="pic-box-2" v-if="linetype === 2"> 
    <div class="column1">
      总金额：<b>￥{{ price }}</b>
    </div>
    <div class="column2" @click="em2">
      结算
    </div>    
  </div>  
  <div class="pic-box-3" v-if="linetype === 3">         
      <slot></slot>
  </div>      
</div>   
  
</template>

<script>
export default {
	name: 'CRLotsbottom',
    componentName: 'CRLotsbottom',

    data() {
      return {
        
      }
    },
 	props: {
 		picsrc:{
      	type: String,
      	default: ''
    },
    linetype:{
        type: Number,
        default: 1
    },
    price:{
      type: Number,
      default: 0
    }
 	},
  	methods:{
  		em(x){
        switch (x)
        {
          case 0:
            alert(0)
            this.$emit('openShop')
          case 1:
            alert(1)
            this.$emit('openCar')
          case 2:
            alert(2)
            this.$emit('addCar')
        }
      },
      em2(x){
        this.$emit('submit')
      }
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
@bh:3.0625rem;
@iw:16.666vw;
@red:#fd5265;
@gray:#bfc0c0;
@gray2:#666464;

body,p,h1,h2,h3,h4,h5,h6,img{
	padding: 0;
	margin:0;
	border:0;
}

img{
	max-width: @iw;
}

  .pic-box{
  	font-size: @fs12;
  	color: #666666;
  	width: @bw;
  	height: @bh;
  	background: #fff;
  	box-sizing: border-box;	
  	display: flex;
  	position: fixed;
  	bottom: 0;
  	left: 0;
  	div{
  		height: 100%;
  	}
  	.column1,.column2,.column3,.column4{
  		display: flex;
      flex-direction: column;
  		justify-content: center;
  		align-items: center;
  	}
  	.column1,.column2{
  		width: 3.875rem;
  		border-right: 1px solid #e5e5e5;
      span{
        display: block;
        width: 1.375rem;
        height: 1.375rem;        
        background-repeat: no-repeat;
        background-size: 100%;
        margin-bottom: 0.2rem;
      }
  	}
    .column1{
      span{
        background-image: url("../../assets/images/new/lots_004.png");
      }
    } 
    .column2{
      span{
        background-image: url("../../assets/images/new/lots_005.png");
      }
    }  	
  	.column3,.column4{
  		width: 7.84375rem;
  		font-size: @fs16;
  	}
  	.column3{
  		color: #333333;
  	}
  	.column4{
  		color: #fff;
  		background: @red;
  	}
  }
  .pic-box-2{
    border-top:1px solid #e5e5e5;
    font-size: @fs12;
    color: #333;
    width: @bw;
    height: @bh;
    line-height: @bh - 0.0625rem;
    background: #fff;
    box-sizing: border-box; 
    display: flex;
    justify-content: space-between;
    position: fixed;
    bottom: 0;
    left: 0;
    div{
      height: 100%;
      line-height: @bh - 0.0625rem;
      font-size: @fs16;
    }
    .column1{
      text-indent: 0.625rem;
    }
    .column2{
      text-align: center;
      background: @red;
      color: #fff;
      width: 6.25rem;
    }
  }
  .pic-box-3{
    font-size: @fs16;
    color: #fff;
    width: @bw;
    height: @bh;   
    line-height:  @bh - 0.0625rem; 
    text-align: center;
    background: @red;
    box-sizing: border-box;
    vertical-align: top;     
    position: fixed;
    bottom: 0;
    left: 0;
  }

</style>


