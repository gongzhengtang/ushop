<template>
	<view class="productSort">
		<Navbar title="分类"></Navbar>
		<view class='aside' :style="{bottom: tabbarH + 'px',height: height + 'rpx'}">
			<scroll-view scroll-y="true" scroll-with-animation='true' style="height: 100%;">
				<view class='item acea-row row-center-wrapper' :class='index==navActive?"on":""'
					v-for="(item,index) in productList" :key="index" @click='tap(index,"b"+index)'>
					<text>{{item.name}}</text>
				</view>
			</scroll-view>
		</view>

		<view class='conter'>
			<scroll-view scroll-y="true" :scroll-into-view="toView" :style='"height:"+height+"rpx;"' @scroll="scroll"
				scroll-with-animation='true'>
				<block v-for="(item,index) in productList" :key="index">

					<view class='listw' :id="'b'+index">
						<view class='title acea-row row-center-wrapper'>
							<view class='line'></view>
							<view class='name'>{{item.name}}</view>
							<view class='line'></view>
						</view>
						<view class='list acea-row'>
							<block v-for="(itemn,indexn) in item.child" :key="indexn">
								<navigator hover-class='none'
									:url='"/pages/goods_list/index?cid="+itemn.id+"&title="+itemn.name'
									class='item acea-row row-column row-middle'>
									<view class='picture' :style="{'background-color':itemn.extra?'none':'#f7f7f7'}">
										<image :src='itemn.extra'></image>
									</view>
									<view class='name line1'>{{itemn.name}}</view>
								</navigator>
							</block>
						</view>
					</view>
				</block>
				<view :style='"height:"+(height-300)+"rpx;"' v-if="number<15"></view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	import Navbar from '@/components/navbar/navbar.vue';
	export default {
		data() {
			return {
				navActive: 0,
				number: "",
				height: 0,
				hightArr: [],
				toView: "",
				tabbarH: 0,
				// 分类数据
				classifyList: [],

				productList: [{
						"id": 515,
						"pid": 0,
						"path": "/0/",
						"name": "每日新品",
						"type": 1,
						"url": "",
						"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/a272fcefed804cf2b1e6785d5662c29ejqjxha0eow.jpg",
						"status": true,
						"sort": 10,
						"child": [{
							"id": 534,
							"pid": 515,
							"path": "/0/515/",
							"name": "玩偶",
							"type": 1,
							"url": "",
							"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/fb364676ea364297b7441638f9e0f557dckg4t2rds.jpg",
							"status": true,
							"sort": 4
						}]
					},
					{
						"id": 245,
						"pid": 0,
						"path": "/0/272/",
						"name": "热门推荐",
						"type": 1,
						"url": "",
						"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/3a395df3d79a40a08cbc938c35e2dc35b84sujo2yn.png",
						"status": true,
						"sort": 0,
						"child": [{
								"id": 246,
								"pid": 245,
								"path": "/0/272/245/",
								"name": "新品上市",
								"type": 1,
								"url": "www",
								"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/8f9eca84e2b14752ad4afb1ab8d06974xua9ambm9y.jpg",
								"status": true,
								"sort": 0
							},
							{
								"id": 248,
								"pid": 245,
								"path": "/0/272/245/",
								"name": "热卖商品",
								"type": 1,
								"url": "www",
								"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/1618a47e11e745ff90c70f752c204e17qi6vjngrcd.jpg",
								"status": true,
								"sort": 0
							},
							{
								"id": 258,
								"pid": 245,
								"path": "/0/272/245/",
								"name": "折扣专区",
								"type": 1,
								"url": "www",
								"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/73f9c6c1b14445b5bb477e8c05d8a2763sfij1gamk.jpg",
								"status": true,
								"sort": 0
							},
							{
								"id": 488,
								"pid": 245,
								"path": "/0/272/245/",
								"name": "精品首发",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/9dcafbf40f4a43909ef991338583e633qh2zl6rdwi.jpg",
								"status": true,
								"sort": 0
							}
						]
					},
					{
						"id": 272,
						"pid": 0,
						"path": "/0/",
						"name": "家用电器",
						"type": 1,
						"url": "",
						"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/37901b98fba74345ad0e8a575999ad09n9d3winw2c.jpg",
						"status": true,
						"sort": 0,
						"child": [{
								"id": 273,
								"pid": 272,
								"path": "/0/272/",
								"name": "电视",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/37901b98fba74345ad0e8a575999ad09n9d3winw2c.jpg",
								"status": true,
								"sort": 0
							},
							{
								"id": 275,
								"pid": 272,
								"path": "/0/272/",
								"name": "洗衣机",
								"type": 1,
								"url": "www",
								"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/62414c551db44169a6429c0dd3d162833o6e82okff.jpg",
								"status": true,
								"sort": 0
							},
							{
								"id": 276,
								"pid": 272,
								"path": "/0/272/",
								"name": "生活电器",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/4811fe50a33f48309337e67c3d36318exseuh6qys6.jpg",
								"status": true,
								"sort": 0
							},
							{
								"id": 277,
								"pid": 272,
								"path": "/0/272/",
								"name": "厨卫电器",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/476f2b8a50644f5f80124f831ac14aecct8ewiyvwf.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 279,
								"pid": 272,
								"path": "/0/272/",
								"name": "清凉一夏",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/f22830611d324e8fb10129e969f1ec661lcpu7346h.png",
								"status": true,
								"sort": 0
							}
						]
					},
					{
						"id": 280,
						"pid": 0,
						"path": "/0/",
						"name": "家装家具",
						"type": 1,
						"url": "",
						"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/86f83bdc35534eeda2fb4daeb51dbb28pizkxqnzap.jpg",
						"status": true,
						"sort": 0,
						"child": [{
								"id": 285,
								"pid": 280,
								"path": "/0/280/",
								"name": "智能门锁",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/8b665c20edef4d61a508de9395eb40c4ln34d0f3i5.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 286,
								"pid": 280,
								"path": "/0/280/",
								"name": "居家照明",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/24119aa4d48e4c7a95b21ece82a41715uns67350bd.jpg",
								"status": true,
								"sort": 0
							},
							{
								"id": 287,
								"pid": 280,
								"path": "/0/280/",
								"name": "家装建材",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/7b4c8af47e414f62a5d7b26d95504cbafw13ela5i7.png",
								"status": true,
								"sort": 0
							}
						]
					},
					{
						"id": 281,
						"pid": 0,
						"path": "/0/",
						"name": "户外出行",
						"type": 1,
						"url": "",
						"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/55014ffb17b74d039b5670298e1047fcyw64lmyzlj.jpg",
						"status": true,
						"sort": 0,
						"child": [{
								"id": 288,
								"pid": 281,
								"path": "/0/281/",
								"name": "健身运动",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/0f419f2a65844ae5a00c20e22dc9b92env32uvr4dy.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 289,
								"pid": 281,
								"path": "/0/281/",
								"name": "户外装备",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/bf8bc87d525844b68ca17ca60c567233hkh2h9c2un.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 290,
								"pid": 281,
								"path": "/0/281/",
								"name": "骑行配件",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/ef98f38ef1cd4083a91fb62b1dd8362cmran1psnmc.png",
								"status": true,
								"sort": 0
							}
						]
					},
					{
						"id": 282,
						"pid": 0,
						"path": "/0/",
						"name": "美妆个护",
						"type": 1,
						"url": "",
						"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/2eef89b403dd47619e349e3edb057ce4g2clr5d4xn.jpg",
						"status": true,
						"sort": 0,
						"child": [{
								"id": 291,
								"pid": 282,
								"path": "/0/282/",
								"name": "美妆工具",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/1ccac5f9f62646ba930000ad70f741efpfgagvhrzh.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 292,
								"pid": 282,
								"path": "/0/282/",
								"name": "口腔清洁",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/0705b0fad3884eddb31745e453de6503atuqud1tr3.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 293,
								"pid": 282,
								"path": "/0/282/",
								"name": "彩妆香氛",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/0e13333fdf2841a2a886a9595bebc855q5jgkr8b66.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 294,
								"pid": 282,
								"path": "/0/282/",
								"name": "面部护肤",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/6246abff834b4d2fb1edad2a8927c8a3yes6irrqfw.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 295,
								"pid": 282,
								"path": "/0/282/",
								"name": "身体护理",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/090f2f83e9b343c38c7c7b4ebc860a352r8u8adjsq.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 296,
								"pid": 282,
								"path": "/0/282/",
								"name": "其他工具",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/fbc798bf3c91493f95c97be7d6cbaa5akhcpo5ent3.png",
								"status": true,
								"sort": 0
							}
						]
					},
					{
						"id": 283,
						"pid": 0,
						"path": "/0/",
						"name": "3C数码",
						"type": 1,
						"url": "",
						"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/432cb941d4f64f4c88d2d3a8b784f282kqlp2cu55l.jpg",
						"status": true,
						"sort": 0,
						"child": [{
								"id": 297,
								"pid": 283,
								"path": "/0/283/",
								"name": "手机",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/73f9c6c1b14445b5bb477e8c05d8a2763sfij1gamk.jpg",
								"status": true,
								"sort": 0
							},
							{
								"id": 298,
								"pid": 283,
								"path": "/0/283/",
								"name": "平板电脑",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/maintain/2021/12/25/4811fe50a33f48309337e67c3d36318exseuh6qys6.jpg",
								"status": true,
								"sort": 0
							}
						]
					},
					{
						"id": 284,
						"pid": 0,
						"path": "/0/283/",
						"name": "日用文创",
						"type": 1,
						"url": "",
						"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/d813cbdd98b148c99885652234ad43b1m1aewwn8wd.jpg",
						"status": true,
						"sort": 0,
						"child": [{
								"id": 300,
								"pid": 284,
								"path": "/0/283/284/",
								"name": "日用杂货",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/61bf8228d96b4c8c9343bc13b4e6fc67c0jmc2y781.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 301,
								"pid": 284,
								"path": "/0/283/284/",
								"name": "纸品湿巾",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/ae2a9db4d74a4a56bddb971d3df9e60fljwxe9z3lh.png",
								"status": true,
								"sort": 0
							},
							{
								"id": 302,
								"pid": 284,
								"path": "/0/283/284/",
								"name": "办公文具",
								"type": 1,
								"url": "",
								"extra": "http://47.97.34.240:8088/crmebimage/public/store/2021/12/25/de35d545523448db9f3636e34ca085b29qw11rescg.png",
								"status": true,
								"sort": 0
							}
						]
					}
				]

			};
		},
		components: {
			Navbar
		},
		onLoad(options) {
			this.getAllCategory();
		},
		methods: {
			infoScroll: function() {
				let that = this;
				let len = that.productList.length;
				let child = that.productList[len - 1] && that.productList[len - 1].child ? that.productList[len - 1]
					.child : [];
				this.number = child ? child.length : 0;

				//设置商品列表高度
				uni.getSystemInfo({
					success: function(res) {
						that.height = (res.windowHeight) * (750 / res.windowWidth) - 98;
					},
				});
				let height = 0;
				let hightArr = [];
				for (let i = 0; i < len; i++) {
					//获取元素所在位置
					let query = uni.createSelectorQuery().in(this);
					let idView = "#b" + i;
					query.select(idView).boundingClientRect();
					query.exec(function(res) {
						let top = res[0].top;
						hightArr.push(top);
						that.hightArr = hightArr
					});
				};
			},
			tap: function(index, id) {
				this.toView = id;
				this.navActive = index;
			},
			getAllCategory: function() {
				let that = this;
				setTimeout(function() {
					that.infoScroll();
				}, 500)
			},
			scroll: function(e) {
				let scrollTop = e.detail.scrollTop;
				let scrollArr = this.hightArr;
				for (let i = 0; i < scrollArr.length; i++) {
					if (scrollTop >= 0 && scrollTop < scrollArr[1] - scrollArr[0]) {
						this.navActive = 0
					} else if (scrollTop >= scrollArr[i] - scrollArr[0] && scrollTop < scrollArr[i + 1] - scrollArr[
							0]) {
						this.navActive = i
					} else if (scrollTop >= scrollArr[scrollArr.length - 1] - scrollArr[0]) {
						this.navActive = scrollArr.length - 1
					}
				}
			},

		}
	};
</script>

<style lang="scss" scoped>
	.acea-row {
		display: -webkit-box;
		display: -moz-box;
		display: -webkit-flex;
		display: -ms-flexbox;
		display: flex;
		-webkit-box-lines: multiple;
		-moz-box-lines: multiple;
		-o-box-lines: multiple;
		-webkit-flex-wrap: wrap;
		-ms-flex-wrap: wrap;
		flex-wrap: wrap
	}

	.acea-row.row-center-wrapper {
		-webkit-box-align: center;
		-moz-box-align: center;
		-o-box-align: center;
		-ms-flex-align: center;
		-webkit-align-items: center;
		align-items: center;
		-webkit-box-pack: center;
		-moz-box-pack: center;
		-o-box-pack: center;
		-ms-flex-pack: center;
		-webkit-justify-content: center;
		justify-content: center
	}

	.productSort .header {
		width: 100%;
		height: 96rpx;
		background-color: #fff;
		position: fixed;
		left: 0;
		right: 0;
		top: 0;
		z-index: 9;
		border-bottom: 1rpx solid #f5f5f5;
	}

	.productSort .header .input {
		width: 700rpx;
		height: 60rpx;
		background-color: #f5f5f5;
		border-radius: 50rpx;
		box-sizing: border-box;
		padding: 0 25rpx;
	}

	.productSort .header .input .iconfont {
		font-size: 26rpx;
		color: #555;
	}

	.productSort .header .input .placeholder {
		color: #999;
	}

	.productSort .header .input input {
		font-size: 26rpx;
		height: 100%;
		width: 597rpx;
	}

	.productSort .aside {
		position: fixed;
		width: 180rpx;
		left: 0;
		top: 0;
		background-color: #f7f7f7;
		overflow-y: scroll;
		overflow-x: hidden;

		height: auto;
		margin-top: 190rpx;
	}

	.productSort .aside .item {
		height: 100rpx;
		width: 100%;
		line-height: 100rpx;
		font-size: 26rpx;
		color: #424242;
	}

	.productSort .aside .item.on {
		background-color: #fff;
		border-left: 4rpx solid #fc4141;
		width: 100%;
		text-align: center;
		color: #fc4141;
		font-weight: bold;

	}

	.productSort .conter {
		margin: 0 0 0 180rpx;
		padding: 0 14rpx;
		background-color: #fff;
	}

	.productSort .conter .listw {
		padding-top: 20rpx;
	}

	.productSort .conter .listw .title {
		height: 90rpx;
	}

	.productSort .conter .listw .title .line {
		width: 100rpx;
		height: 2rpx;
		background-color: #f0f0f0;
	}

	.productSort .conter .listw .title .name {
		font-size: 28rpx;
		color: #333;
		margin: 0 30rpx;
		text-align: center;
		font-weight: bold;
	}

	.productSort .conter .list {
		flex-wrap: wrap;
	}

	.productSort .conter .list .item {
		width: 177rpx;
		margin-top: 26rpx;
	}

	.productSort .conter .list .item .picture {
		width: 120rpx;
		height: 120rpx;
		border-radius: 50%;
	}

	.productSort .conter .list .item .picture image {
		width: 100%;
		height: 100%;
		// border-radius: 50%;

		div {
			background-color: #f7f7f7;
		}
	}

	.productSort .conter .list .item .name {
		font-size: 24rpx;
		color: #333;
		height: 56rpx;
		line-height: 56rpx;
		width: 120rpx;
		text-align: center;
	}
</style>