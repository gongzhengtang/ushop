<template>
	<view class="page">
		<view class="nav-swiper">
			<!-- 带城市、搜索框的导航栏 -->
			<navbar-city-search placeholder="搜索商品、品牌" :cityListSelected="nowSelectedCity"
				class="nav-city"></navbar-city-search>

			<!-- 轮播图 -->
			<view class="banner-swiper"><u-swiper height="300rpx" :list="bannerSwiperList" mode="round" name="pic"
					border-radius="0"></u-swiper></view>
		</view>

		<!-- 金刚区 -->
		<view class="dial-nav"><dial-nav imgSize="88rpx" :list="dialNavList" imgName="pic" :mode="10"></dial-nav></view>

		<!-- 海报区 -->
		<Poster></Poster>
		<!-- 推荐商品 -->
		<view class="recommendGoods">
			<!-- 带操作的标题组件 -->
			<TitleOperate title="推荐商品" showMore></TitleOperate>
			<view class="list">
				<!-- 瀑布流组件 -->
				<u-waterfall ref="topicWaterFall" v-model="recommendGoodsList" marginLeft="7rpx" marginRight="7rpx">
					<template v-slot:left="{ leftList }">
						<CardGoods v-for="(item, index) in leftList" :key="index" :data="item"></CardGoods>
					</template>
					<template v-slot:right="{ rightList }">
						<CardGoods v-for="(item, index) in rightList" :key="index" :data="item"></CardGoods>
					</template>
				</u-waterfall>
			</view>
		</view>
		<!-- 精选晒单 -->
		<view class="recommendTopic ">
			<!-- 带操作的标题组件 -->
			<TitleOperate title="精选晒单"></TitleOperate>
			<view class="list">
				<!-- 瀑布流组件 -->
				<u-waterfall ref="topicWaterFall" v-model="recommendTopicList" marginLeft="7rpx" marginRight="7rpx">
					<template v-slot:left="{ leftList }">
						<PostCardSimple v-for="(item, index) in leftList" :key="index" :data="item">
						</PostCardSimple>
					</template>
					<template v-slot:right="{ rightList }">
						<PostCardSimple v-for="(item, index) in rightList" :key="index" :data="item">
						</PostCardSimple>
					</template>
				</u-waterfall>
			</view>
		</view>
	</view>
</template>

<script>
	// 导入组件
	import NavbarCitySearch from '@/components/navbar/navbar-city-search.vue';
	import DialNav from '@/components/nav/dial-nav.vue';
	import HorizontalScrollNav from '@/components/nav/horizontal-scroll-nav.vue';
	import CardGoods from '@/pages/cart/components/card.vue';
	import PostCardSimple from '@/pages/community/components/post-card-simple.vue';
	import TitleOperate from '@/components/title-operate.vue';
	import Poster from '@/pages/home/components/poster.vue';
	import Points from '@/pages/home/components/points.vue';
	// 导入假数据
	import {
		goodsList,
		topicList,
		bannerSwiperList,
		dialNavList,
		pointsList
	} from '@/static/test-data.js';

	export default {
		components: {
			NavbarCitySearch,
			DialNav,
			HorizontalScrollNav,
			CardGoods,
			PostCardSimple,
			TitleOperate,
			Poster,
			Points
		},
		data() {
			return {
				// 轮播图
				bannerSwiperList: bannerSwiperList,
				// 金刚区
				dialNavList: dialNavList,
				// 积分兑换
				pointsList: pointsList,
				// 由城市选择页面返回的选择城市数据
				nowSelectedCity: '',
				// 推荐商品列表
				recommendGoodsList: [],
				// 精选晒单列表
				recommendTopicList: []
			};
		},
		onShow() {
			// 处理是否手动选择了城市
			let nowSelectedCity = uni.getStorageSync('NOW_SELECTED_CITY');
			if (nowSelectedCity) {
				this.nowSelectedCity = nowSelectedCity;
				uni.clearStorageSync('NOW_SELECTED_CITY');
			}
			// 处理首页需要渲染的数据
			this.loadPageData(false);
		},
		methods: {
			// 首页需要渲染的数据
			loadPageData(isAll = true) {
				setTimeout(() => {
					this.getRecommendGoods();
					this.getRecommendTopic();
				}, 0);
			},

			// 加载推荐商品
			getRecommendGoods() {
				this.$nextTick(() => {
					this.recommendGoodsList = JSON.parse(JSON.stringify(goodsList));
				});
			},

			// 加载精选帖子
			getRecommendTopic() {
				this.$nextTick(() => {
					this.recommendTopicList = JSON.parse(JSON.stringify(topicList));
				});
			},

			// 去购物粗
			goShoppingCart() {
				uni.navigateTo({
					url: '/pages-mall/pages/shopping-cart'
				});
			}
		}
	};
</script>

<style lang="scss" scoped>
	.banner-swiper {
		padding: 10rpx 30rpx 0 30rpx;
		background-color: $app-theme-bg-color;
		height: 300rpx;
	}

	.recommendGoods {
		.list {
			padding: 0 30rpx;
		}
	}

	.list {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		padding: 0 30rpx;
	}

	.dial-nav {
		padding: 24rpx 30rpx 30rpx 30rpx;
	}
</style>