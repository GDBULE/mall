<template>
	<div id="tab-bar">
		<slot></slot>
	</div>
</template>

<script>
	export default {
		name:"TabBar",
	}
</script>

<style scoped>
	#tab-bar{
		  background-color: #F6F6F6;
		  display: flex;
		  box-shadow: 0 -1px 1px rgba(100,100,100,0.15 );
		  position: fixed;
		  right: 0;
		  left: 0;
		  bottom: 0;
	}
</style>
