<template>   

  <div class="pic-box">  	
	<div class="pic-zone">
		<img :src="picsrc" alt="">
	</div>
	<div class="word-zone">
		<p><slot name="row1"></slot></p>
		<p><slot name="row2"></slot></p>
	</div>	
  </div>      

</template>

<script>
export default {
	name: 'CRPiclinegray',
    componentName: 'CRPiclinegray',

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
	    // 'picsrc': 'picFun'	    
  	},
  	mounted(){
  		console.log(this.picsrc)
  	},
  	methods:{
  		picFun(){
  			console.log(this.picsrc)
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
@bh:4.375rem;
@iw:3.125rem;
@gray:#bfc0c0;
@gray2:#666464;
@gray3:#f5f5f5;
@black1:#333232;
@red:#fd5265;

body,p,h1,h2,h3,h4,h5,h6,img{
	padding: 0;
	margin:0;
	border:0;
}

img{
	max-width: @iw;
}

	.pic-box-f{
		width: @bw;
		height: @bh;
		padding: 0 @pd1;
		background: #fff;
		box-sizing: border-box;
	}
	.pic-box{
		color: #333;
		width: 100%;
		height: @bh;
		background: @gray3;
		box-sizing: border-box;
		padding: @pd1 @pd1;
		display: flex;	
	}
	.pic-zone{
		width: @iw;
		height: @iw;
		overflow: hidden;		
		margin-right: @pd1;
	}
	.word-zone{
		font-size: @fs16;
		display: flex;
		flex-direction:column;
		justify-content:center;
		color: #333;		
		p:first-child{
			padding-bottom: 1vw;				
		}
		p:last-child{			
			color: #999999;
			font-size: @fs14;		
		}
	}	
</style>


