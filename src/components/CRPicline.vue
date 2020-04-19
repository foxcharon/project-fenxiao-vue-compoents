<template>   
<div>
  <div class="pic-box" v-if="linetype === 1">  	
	<div class="pic-zone">
		<img :src="picsrc" alt="">
	</div>
	<div class="word-zone">
		<p><slot name="row1"></slot></p>
		<p><slot name="row2"></slot></p>
	</div>	
  </div>   
  <div class="pic-box noborder" v-if="linetype === 2">  	
	<div class="pic-zone">
		<img :src="picsrc" alt="">
	</div>	
	<div class="word-zone-2">
		<p><slot name="row1"></slot></p>
		<p><slot name="row2"></slot></p>
	</div>
  </div>
  <div class="pic-box" v-if="linetype === 3">  	
	<div class="pic-zone">
		<img :src="picsrc" alt="">
	</div>	
	<div class="word-zone-3">
		<p><slot name="row1"></slot></p>
		<p><slot name="row2"></slot></p>
		<p><slot name="row3"></slot></p>
	</div>
  </div>      
</div>
</template>

<script>
export default {
	name: 'CRPicline',
    componentName: 'CRPicline',

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
	    }
 	},
 	watch: {	    
	    'picsrc': 'picFun'	    
  	},
  	mounted(){
  		// console.log(this.picsrc)
  	},
  	methods:{
  		picFun(){
  			// console.log(this.picsrc)
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
div,span,p{
	font-size: @fs12;
}
img{
	max-width: @iw;
}

  .pic-box{
  	color: #333;
  	width: @bw;
  	height: @bh;
  	background: #fff;
  	box-sizing: border-box;
	padding: @pd2 @pd1;
	display: flex;
	border-bottom: 1px solid #efefef;
	&.noborder{
		border:0;
	}
  }
  .pic-zone{
  	width: @iw;
  	height: @iw;
  	overflow: hidden;
  	border-radius: 4px;
  	margin-right: @pd1;
  }
  .word-zone{
  	font-size: @fs12;
  	display: flex;
  	flex-direction:column;
  	justify-content:center;
	p{
		color: @gray;		
		span:nth-child(2){			
			transform: translateY(-0.1vw);
			display: inline-block;
			color: @gray2;
		}
	}
	p:first-child{
		padding-bottom: 3vw;
		span:first-child{			
			font-size: @fs16;
			color: @gray2;
		}		
	}
	p:last-child{
		span:first-child{
			color: #333;
			font-size: @fs16;
			transform: translateY(-0.1vw) translateX(0.9vw) scale(1.3,1.3);
			display: inline-block;
			margin-right: 2.5vw;
			font-weight: 700;
		}
	}
  }
  .word-zone-2{
  	font-size: @fs12;
  	display: flex;
  	flex-direction:column;
  	justify-content:center;
  	p{
  		color: @black1;
  		font-size: @fs14;
  		span{
  			color: @gray;
  			b{
				font-size: @fs20;
				color: @red;
				font-weight: 700;
				transform: translateY(0.3vw);
				display: inline-block;
  			}
  		}
  	}
  }
  .word-zone-3{
  	font-size: @fs14;
  	color: #666;
  	display: flex;
  	flex-direction:column;
  	justify-content:space-between;
  	p{
  		&:first-child{
  			color: #333;
  			font-size: @fs15;  			
  		}
  		&:nth-child(2){
  			
  		}
  	}  	
  }
</style>


