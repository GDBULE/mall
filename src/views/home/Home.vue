<template>
	<div id="home">
		<nav-bar class="home-nav-bar">
			<div slot="center">购物街</div>
		</nav-bar>
		<scroll class="content" ref="scroll" :probe-type="3" @scroll="contentScroll">
			<home-swiper :cbanners="banners"></home-swiper>
			<home-recommend :crecommends="recommends"></home-recommend>
			<home-feature-view></home-feature-view>
			<tab-control :titles="['流行' , '新款' , '精选']" @tabClick="tabClick"></tab-control>
			<goods-list :cgoods="showGoods"></goods-list>
		</scroll>
		
		<back-top @click.native="backClick" v-show="showBackTop"/>
	</div>
</template>

<script>
	import HomeSwiper from './childComps/HomeSwiper.vue'
	import HomeRecommend from './childComps/HomeRecommend.vue'
	import HomeFeatureView from './childComps/HomeFeatureView.vue'
	
	import NavBar from 'components/common/navbar/NavBar'
	import TabControl from 'components/content/tabControl/TabControl'
	import GoodsList from 'components/content/goods/GoodsList'
	import Scroll from 'components/common/scroll/Scroll'
	import BackTop from 'components/content/backTop/BackTop'
	
	import {getHomeMultiData , getHomeGoods} from 'network/home.js'
	
	export default {
		name:"Home",
		components:{
			NavBar,
			HomeSwiper,
			HomeRecommend,
			HomeFeatureView,
			TabControl,
			GoodsList,
			Scroll,
			BackTop
		},
		
		data(){
			return {
				banners:[],
				recommends:[],
				goods:{
					'pop':{ page:0 , list:[] },
					'new':{ page:0 , list:[] },
					'sell':{ page:0 , list:[] }
				},
				
				currentType:'pop',
				showBackTop:false
			}
		},
		computed:{
			showGoods(){
			return this.goods[this.currentType].list
			}
		},
		created(){
			this.getHomeData()
			this.getHomeGoods('pop')
			this.getHomeGoods('new')
			this.getHomeGoods('sell')
		},
		methods:{
			//事件点击相关方法
			tabClick(index){
				switch(index){
					case 0:
					this.currentType = 'pop'
					break;
					case 1:
					this.currentType = 'new'
					break;
					case 2:
					this.currentType = 'sell'
					break;
					
				}
			},
			backClick(){
				this.$refs.scroll.scrollTo(0,0)
			},
			contentScroll(position){
				// console.log(position)
			    this.showBackTop = (-position.y) > 1000 
			},
			
			//网络请求相关方法
			getHomeData(){
				getHomeMultiData().then(res => {
					// console.log(res);
					this.banners = res.data.banner.list;
					this.recommends = res.data.recommend.list;
				})
			},
			getHomeGoods(type){
				const page = this.goods[type].page+1;
				getHomeGoods(type , page).then(res => {
					// console.log(res);
					this.goods[type].list.push(...res.data.list);
					this.goods[type].page+1;
				})
			},
			
			
			
		}
		
	}
</script>

<style scoped>
	#home{
		position: relative;
		height: 100vh;
		/* padding-top: 44px; */
		/* background-color: #42B983; */
	}
	.home-nav-bar{
		background-color: var(--color-tint);
		color:#fff;
		
		position: fixed;
		left: 0;
		right: 0;
		top: 0;
		z-index: 9;
	}
	/* .content{
		height: calc(100% - 93px);
		overflow: hidden;
		margin-top: 44px;
		
	} */
	
	.content{
		overflow: hidden;
		position: absolute;
		top: 44px;
		bottom: 49px;
		left: 0;
		right: 0;
		
	}
</style>
