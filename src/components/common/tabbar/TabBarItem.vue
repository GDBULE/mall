<template>
	<div class="tab-bar-item" @click="itemClick">
		<!-- <img src="../../assets/img/tabbar/wode.jpg" alt="我的">
		<div>首页</div> -->
		<div v-if="!isActive"><slot  name="item-icon"></slot></div>
		<div v-else><slot name="item-icon-active"></slot></div>
		<div :style="isStyleActive"><slot name="item-text"></slot></div>
	</div>
	
</template>

<script>
	export default{
		name:"TabBarItem",
		props:{
			path:{
				type:String
			},
			activeColor:{
				type:String,
				default:'#ff3c4f'
			}
		},
		data(){
			return{
				
			}
		},
		computed:{
			isActive(){
				return this.$route.path.indexOf(this.path) !==-1
			},
			
			isStyleActive(){
				return this.isActive ? { color:this.activeColor } : {}
			}
		},
		methods:{
			itemClick(){
				// console.log("你好")
				this.$router.replace(this.path)
			}
			
		}
	}
</script>

<style>
	
	.tab-bar-item{
		  flex: 1 ;
		  text-align: center;
		  height: 49px;
		  font-size: 14px;
	}
	
	.tab-bar-item img{
		width: 22px;
		height: 22px;
		margin-top: 3px;
		margin-bottom: 1px;
		vertical-align: middle;
	}
	
</style>
