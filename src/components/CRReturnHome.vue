<template>   
	<div class="return" @click="home">
		<img src="../../assets/images/new/return.png" alt="">       
	</div>
</template>

<script>
export default {
	name: 'CRReturnHome',
    componentName: 'CRReturnHome',

    data() {
      return {
        
      }
    },
 	props: {
 		
 	},
 	watch: {	    
	    'picsrc': 'picFun'	    
  	},
  	mounted(){
  		
  	},
  	methods:{
  		picFun(){
  			
  		},
  		home(){
  			this.$router.push('/Index')
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

.return{
	position: fixed;
	right: 0;
	top:320px;
	width: 40px;
	height: 55px;
	img{
		width: 100%;
		height: 100%;
	}
}
</style>


