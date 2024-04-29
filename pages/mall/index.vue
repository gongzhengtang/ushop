<template>
	<view class="page">
		<Navbar title="分类"></Navbar>
		<!-- 搜索 -->
		<!-- <view class="sarch">
			<u-search placeholder="商品/品牌"></u-search>
		</view> -->
		<view class="inner">
			<!-- 侧栏 -->
			<view class="aside">
				<view class="item acea-row row-center-wrapper" :class="categoryDivindex === sideIndex ? 'on' : ''"
					v-for="(item, categoryDivindex) in classifyList" :key="categoryDivindex"
					@click="changeSide(categoryDivindex)">
					{{ item.cateName }}
				</view>
			</view>
			<!-- 主内容 -->
			<scroll-view class="conter" scroll-y="true">
				<view v-for="(item, index) in classifyList" :key="index">
					<view class="recommendGoods" v-if="index == sideIndex">
						<view class="list">
							<u-waterfall ref="topicWaterFall" v-model="item.children" marginLeft="7rpx"
								marginRight="7rpx">
								<template v-slot:left="{ leftList }">
									<CardGoods v-for="(data, i) in leftList" :key="i" :data="data">
									</CardGoods>
								</template>
								<template v-slot:right="{ rightList }">
									<CardGoods v-for="(data, i) in rightList" :key="i" :data="data">
									</CardGoods>
								</template>
							</u-waterfall>
						</view>

						<NoData height="50vh" v-if="item.children.length == 0"></NoData>
					</view>
				</view>
			</scroll-view>
		</view>

	</view>
</template>

<script>
	import Navbar from '@/components/navbar/navbar.vue';
	import CardGoods from '@/pages/cart/components/card.vue';
	import {
		goodsList
	} from '@/static/test-data.js';
	export default {
		data() {
			return {
				// 分类数据
				classifyList: [],
				// 分类索引
				sideIndex: 0,
				// 传参id
				queryClassifyId: ''

			};
		},
		components: {
			Navbar,
			CardGoods
		},
		onLoad(options) {
			if (options.id) {
				this.queryClassifyId = options.id;
			}
			this.getClassifyList();
		},
		methods: {
			// 动态切换分类
			changeClassifyById() {
				let nowClassifyIndex = 0;
				if (!this.queryClassifyId) return;
				this.classifyList.forEach((item, index) => {
					if (item.id === this.queryClassifyId) nowClassifyIndex = index;
				});
				if (nowClassifyIndex !== this.navActive) {
					this.changeSide(index);
				}
			},

			// 查询分类列表
			getClassifyList() {
				this.classifyList = [{
						cateName: '推荐',
						children: JSON.parse(JSON.stringify(goodsList))
					},
					{
						cateName: '百货',
						children: JSON.parse(JSON.stringify(goodsList))
					},
					{
						cateName: '服饰',
						children: JSON.parse(JSON.stringify(goodsList))
					},
					{
						cateName: '运动',
						children: JSON.parse(JSON.stringify(goodsList))
					}
				];
				this.changeClassifyById();
			},

			// 切换分类
			changeSide(index) {
				this.sideIndex = index;
			},

			// 跳转商品列表页
			goGoodsList(child) {
				this.$u.route('/pages-mall/pages/goods/list', {
					id: child.id
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
	// .list {
	// 	display: flex;
	// 	flex-wrap: wrap;
	// 	justify-content: space-between;
	// 	padding: 0 30rpx;
	// }

	.page {
		background: $app-theme-bg-color;


		.sarch {
			padding: 24rpx 30rpx 0rpx 30rpx;
		}

		.inner {
			display: flex;
			justify-content: space-between;
			align-items: flex-start;

			.aside {
				width: 196rpx;
				background: $app-theme-bg-gray-color;
				height: 100%;

				.item {
					height: 100rpx;
					line-height: 100rpx;
					text-align: center;
					font-size: 32rpx;
					font-family: PingFang-SC-Medium, PingFang-SC;
					font-weight: 500;
					color: $app-theme-text-black-color;
					transition: all 0.3s ease-in-out;

					&.on {
						color: $app-theme-color;
						position: relative;
						background-color: $app-theme-bg-color;
						transition: all 0.3s ease-in-out;

						&::before {
							position: absolute;
							top: 50%;
							left: 0;
							transform: translate(0, -50%);
							content: '';
							height: 30rpx;
							width: 8rpx;
							background-color: $app-theme-color;
						}
					}
				}
			}

			.conter {
				padding: 30rpx 40rpx 30rpx 40rpx;

				.recommendGoods {
					.list {
						padding: 0 30rpx;
					}
				}
			}
		}
	}
</style>