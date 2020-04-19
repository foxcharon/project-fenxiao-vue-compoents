<template>   
  <div class="pic-box" @click="em">
  	<p class="pic-zone" @click="em2">
  		<img :src="picsrc" alt="">
  	</p>
  	<div class="word-zone">  
	    <p class="p1"><slot name="row1"></slot></p>
	    <p>
	    	<span class="p2">
	    		<slot name="row2"></slot>
	    	</span>
	    	<span class="p3">
	    		<slot name="row2-2"></slot>
	    	</span>
		</p>
		<p class="p4"><del><slot name="row3"></slot></del></p>
	</div>
	<slot name="free"></slot>
  </div>   
</template>

<script>
export default {
	name: 'CRPicbox',
    componentName: 'CRPicbox',

    data() {
      return {
        
      }
    },
 	props: {
 		picsrc:{
	      	type: String,
	      	default: ''
	    }
 	},
 	watch: {	    
	    'picsrc': 'picFun'	    
  	},
  	mounted(){
  		// console.log(this.picsrc)
  	},
  	methods:{
  		em(){
	      this.$emit('open');
	    },
	    em2(){
	      this.$emit('picopen');
	    }
  	}
 	
}
</script>

<style lang="less" scoped>
@fs14:3.733vw;
@fs15:4vw;
@fs12:3.2vw;
@pd1:2.666vw;
@bw:46vw;
@bh:64.533vw;
body,p,h1,h2,h3,h4,h5,h6,img{
	padding: 0;
	margin:0;
	border:0;
}
div,span,p{
	font-size: @fs12;
}
img{
	max-width: @bw;
}

  .pic-box{
  	position: relative;
  	color: #333;
  	width: @bw;
  	height: @bh;
  	background: #fff;
  	margin-bottom: @pd1;
  }
  .pic-zone{
  	width: @bw;
  	height: @bw;
  	overflow: hidden;
  }
  .word-zone{
  	font-size: @fs12;
  	padding: 2.667vw 2vw 0; 
	.p1{
		font-size: @fs15;
		font-weight: 700;
		padding-bottom: 1vw;
	}
	.p2{
		color:#bfc0c0;
	}
	.p3{
		display: inline-block;
		color:#f80c53;
		font-weight: 700;
		transform: scale(1.3,1.3) translateY(-0.25vw);
	}
	.p4{
		font-style: italic;
		color: #c1c1c1;
	}
  }
</style>


