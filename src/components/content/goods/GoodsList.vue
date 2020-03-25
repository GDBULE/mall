<template>
	<div class="goods">
		<goods-list-item v-for="item in cgoods" :goods-item="item"></goods-list-item>
		
	</div>
</template>

<script>
	import GoodsListItem from './GoodslistItem.vue'
	export default {
		name:"GoodsList",
		components:{
			GoodsListItem
		},
		props:{
			cgoods:{
				type:Array,
				default(){
					return []
				}
			}
		}
	}
</script>

<style scoped>
	.good-list {
	  display: flex;
	  flex-wrap: wrap;
	  justify-content: space-around;
	  background-color: var(--color-background);
	
	  padding: 2px;
	}
</style>
