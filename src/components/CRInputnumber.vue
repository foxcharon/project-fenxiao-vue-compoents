<template>   
  <div class="input-number">  	
	<div @click="sub" :class="(islight ? 'light' : '') + ' sub'">-</div>
	<div class="num">{{ ipt }}</div>
	<div class="add" @click="add">+</div>
  </div>   
</template>

<script>
import { qs, change_goods_num } from '@/api.js'
export default {
	name: 'CRInputnumber',
    componentName: 'CRInputnumber',

    data() {
      return {
        ipt:parseInt(this.count),
        islight: true,
      }
    },
    created() {   	
    	this.islight = this.lightFunc()
    },
 	props: {
 		count:{
	      	type: Number,
	      	default: 1
	    },
	    id:{
	      	type: String,
	      	default: 1
	    }
 	},
 	watch:{
      	
    },
 	methods: {
	// 减少数量
		sub: function () {
			if (this.ipt < 2) {
				return
			}
			this.ipt--
			this.calc('add')			
		},
		// 增加数量
		add: function () {
		    this.ipt++
		    this.calc('sub')		    
		},
		lightFunc(){
			if (this.ipt < 2) {
				return true
			} else {
				return false
			}
		},
		calc(ac){
			console.log('calc')
			let para = {
				goodsid:this.id,
				action:ac
			}
			this.$http.post(change_goods_num, qs.stringify(para)).then((res) => {
				console.log(res.data)
				if (res.data.code === 200) {
					this.ipt = parseInt(res.data.data.obj.goodsNum)
				} else {
					this.ipt = parseInt(this.ipt)
				}
				this.submit()
			})			
		},
		submit(){
			this.islight = this.lightFunc()
			this.$emit('changeNumber', this.ipt)
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
@black:#4c4948;
@gray:#bfc0c0;

body,p,h1,h2,h3,h4,h5,h6,img{
	padding: 0;
	margin:0;
	border:0;
}
div,span,p{
	font-size: @fs12;
}
	.input-number{
		color: @black;
		font-size: @fs20;
		
		min-width: 4.5625rem;
		height: 1.375rem;
		box-sizing: border-box;
		border: 1px solid #e5e5e5;
		position: relative;
		margin-top: -0.6875rem;
		top:50%;
		display: flex;
		justify-content: space-between;
		.sub,.add,.num{
			height: 100%;
			line-height: 1.25rem;
			text-align: center;
		}
		.sub,.add{
			width: 1.375rem;				
			transform: scale(1.5,1.5) translateY(-0.3vw);		
		}
		.num{
			border-left:1px solid #e5e5e5;
			border-right:1px solid #e5e5e5;
			padding: 0 0.6rem;
			font-weight: 700;
		}
		.sub{
			
		}
		.add{
			
		}
		.light{
			color: #e5e5e5;
		}
	}

</style>


