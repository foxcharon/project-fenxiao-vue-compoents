<template>   
	<div :class="'list-single ' + (noborder ? ' noborder' : '')" @click="em">
	  <div :class="'fff ' + (boldLeft ? ' bold' : '')">
      <slot name="left"></slot>
    </div>
	  <div :class="'fff ' + (gray ? ' gray' : '') + (red ? ' red' : '') + (bold ? ' bold' : '')">
      <slot name="right"></slot>
    </div>
    <div class="afterarrow" v-if="arrow === true"></div>
	</div>
</template>

<script>
export default {
	name: 'CRListsingle',
    componentName: 'CRListsingle',

    data() {
      return {
        
      }
    },
 	props: {  
      noborder: {
        type: Boolean,
        default: false
      },  
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
      arrow: {
        type: Boolean,
        default: false
      },
      boldLeft: {
        type: Boolean,
        default: false
      },
 	},
  methods:{
    em(){
      this.$emit('open');
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

img{
	max-width: @iw;
}

  .list-single{
    position: relative;
  	height: 3.75rem;
  	line-height: 3.75rem;
  	display: flex;
  	justify-content: space-between;
  	padding: 0 @pd1;
  	color: #333;
  	font-size: @fs16; 
  	border-bottom: 1px solid #e5e5e5;
  	&:last-child{
  		border:0;
  	}  
    &.noborder{
      border:0;
    } 	
  	.gray{
  		color: #999999;
  	}
    .red{
      color: @red;
    }
    .bold{
      font-weight: 700;
    }  
  }
  .afterarrow{
    position: absolute;
    width: 0.40625rem;
    height: 0.625rem;          
    top:43%;
    right: 0.625rem;
    background-image: url("../../assets/images/new/ordersubmit_001.png");
    background-repeat: no-repeat;
    background-size: 100%;
  }  
  
</style>


