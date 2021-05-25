# 简介
uniapp

本插件适用方便提示请求的信息，使用起来方便，可以后期二期开发

这是一个项目下载地址链接 [github](https://github.com/lizhizhong/popView)

# 兼容说明
适合所有前端组件


# 导入
```
import navc from '../../components/self-navc/navc.vue';
```



# 使用案例
```
<template>
	<view id="content">
		<navc></navc>
		<view class="content">
			<view class="topView">
				<view class="topL">
					<image src="../../static/logo.png"></image>
				</view>
				<view class="topC">
					<text class="title">古典舞·第一阶</text>
					<text class="status">已结束|25人</text>
				</view>
				<view class="topR">
					<text class="attention">+关注</text>
				</view>
			</view>
			<view class="courseVideo">
				<view class="videoView">
					<view id="tcView" ref="tcView" class="video-container">
						<image src="../../static/default.png"></image>
					</view>
				</view>

			</view>
			<view class="selectItem detail" id="detail">
				<scroll-view class="scrollview title" id="title" :scroll-x="true" :style="slide?'position:relative;top:0px;width:'+pageWidth+'px':'position:fixed;top:'+top+'px;width:'+pageWidth+'px'">
					<view class="line" :style='"transform:translateX("+isLeft+"px);width:"+isWidth+"px"'></view>
					<view id="item1" class="items" @click="clickItem('#item1',1)">
						<text :class="current_index==1?'selected':''">介绍</text>
					</view>
					<view id="item2" class="items" @click="clickItem('#item2',2)">
						<text :class="current_index==2?'selected':''">排行</text>
					</view>
					<view id="item3" class="items" @click="clickItem('#item3',3)">
						<text :class="current_index==3?'selected':''">授课</text>
					</view>
					<view id="item4" class="items" @click="clickItem('#item4',4)">
						<text :class="current_index==4?'selected':''">讨论</text>
					</view>
				</scroll-view>
			</view>
			<view id="itemAll" class="itemAll">
				<swiper class="swiper" :current="current" @change="change">
					<swiper-item>
						<scroll-view class="swiper-item1 component" scroll-y="true">
							<view class="one">
								<view class="body">
									<view class="course">
										<view class="title">
											<text>第十一课 童话王国</text>
										</view>
										<view class="time">
											<text>2020-07-05 19:00:00开始直播</text>
										</view>
									</view>
									<view class="contentA">
										<scroll-view class="scrollviewA" :scroll-x="true">
											<view class="lineA" :style='"transform:translateX("+isLeftA+"px);width:"+isWidthA+"px"'></view>
											<view id="item1A" class="itemsA" @click="clickItemA('#item1A',1)">
												<text :class="currentA_index==1?'selected':''">详情</text>
											</view>
											<view id="item2A" class="itemsA" @click="clickItemA('#item2A',2)">
												<text :class="currentA_index==2?'selected':''">讲师</text>
											</view>
										</scroll-view>
									</view>
									<view id="itemAllA" class="itemAllA">
										<swiper class="swiper" :current="currentA" @change="changeA">
											<swiper-item>
												<scroll-view class="swiper-item1 component" scroll-y="true">
													<view class="one">
														11
													</view>
												</scroll-view>
											</swiper-item>
											<swiper-item>
												<scroll-view class="swiper-item2 component" scroll-y="true">
													<view class="two">
														22
													</view>
												</scroll-view>
											</swiper-item>
									
										</swiper>
									</view>
								</view>
							</view>
						</scroll-view>
					</swiper-item>
					<swiper-item>
						<scroll-view class="swiper-item2 component" scroll-y="true">
							<view class="two">
								22
							</view>
						</scroll-view>
					</swiper-item>
					<swiper-item>
						<scroll-view class="swiper-item3 component" scroll-y="true">
							<view class="three">
								33
							</view>
						</scroll-view>
					</swiper-item>
					<swiper-item>
						<scroll-view class="swiper-item4 component" scroll-y="true">
							<view class="four">
								44
							</view>
						</scroll-view>
					</swiper-item>

				</swiper>
			</view>

		</view>
		<view class="botttomView position" style="height: buttonViewHeight+'upx';">

		</view>
	</view>
</template>

<script>
	import navc from '../../components/self-navc/navc.vue';
	export default {
		components: {
			navc
		},
		data() {
			return {
				isLeft: 0,
				isLeftA: 0,
				isWidth: 20,
				isWidthA: 20,
				current_index: 1,
				currentA_index: 1,
				player: null,
				playerId: 'videoDomId',
				buttonViewHeight: 0,
				titleHeight: 0, //选择标题的高度
				slide: true, //是否允许滑动
				pageWidth: 0, //页面宽度
				top: 0, //向滚动的位置
				currentIndex: 1, //当先选择
				current: 0, //当前所在滑块的 index
				currentA: 0, //当前所在滑块的 index
			}
		},
		onPageScroll: function(e) { //nvue暂不支持滚动监听，可用bindingx代替
			/* console.log("滚动距离为：" + e.scrollTop);
			console.log(this.getSystemMsg('windowHeight')); */
			if (e.scrollTop + this.navcHeight> this.topDistance) {
				if (this.slide == true) {
					this.slide = false;
				}
		
			} else {
				if (this.slide == false) {
					this.slide = true;
				}
			}
		},
		onLoad(options) {

		},
		/*实例被挂载完成后执行的代码*/
		mounted() {
			this.clickItem('#item1', 1);
			this.clickItemA('#item1A', 1);
			this.getInfo();
		},
		onReady() { //页面初次渲染完毕执行
			
		},
		destroyed() {
			this.player.pause();
			this.player.dispose();
			this.player = null
		},
		methods: {
			getInfo() {
				let rectNavc = this.getViewRect('#topView'); //导航的位置
				this.top = rectNavc.bottom;
				this.navcHeight = rectNavc.height;
				let rectTitle = this.getViewRect('#title');
				this.topDistance = rectTitle.top;
				this.titleHeight = rectTitle.height;
				let rectDetail = this.getViewRect('#detail');
				this.pageWidth = rectDetail.width;
			},
			/*选择导航标题*/
			clickItem(id, index) {
				this.current = index - 1;
				this.current_index = index;
				let rectNavc = this.getViewRect(id); //导航的位置
				let contentNavc = this.getViewRect('#content');
				this.isLeft = rectNavc.left + rectNavc.width / 2.0 - this.isWidth / 2.0 - contentNavc.left;
			},
			clickItemA(id, index) {
				console.log('dddd')
				this.currentA = index - 1;
				this.currentA_index = index;
				let rectNavc = this.getViewRect(id); //导航的位置
				let contentNavc = this.getViewRect('#content');
				this.isLeftA = rectNavc.left + rectNavc.width / 2.0 - this.isWidthA / 2.0 - contentNavc.left;
			},
			/*左右滑动事件*/
			change(e) {
				let current = e.detail.current;
				current++;
				this.clickItem(`#item${current}`, current);
			},
			/*左右滑动事件*/
			changeA(e) {
				let currentA = e.detail.current;
				currentA++;
				this.clickItemA(`#item${currentA}A`, currentA);
			},
			//获取页面坐标
			getViewRect:function(className){
				// 注意：想要拿到元素实例，需要在实例已经挂载到页面上才可以
				var result = 0;
				const query = uni.createSelectorQuery().in(this);
				query.select(className).boundingClientRect(data => {
					// console.log(data)
					result = data;
					
				}).exec();
				return result;
			},
		}
	}
</script>

<style lang="scss">
	page {
		position: relative;

	}

	.content {
		width: 100%;

		margin: 90upx 0 0upx 0;

		// background-color: red;

		box-sizing: border-box;
	}

	.content .topView {
		width: auto;
		height: 90upx;

		display: flex;

		margin-bottom: 1upx;
		padding: 10upx;

		background-color: #fff;
	}

	.content .topView .topL {
		width: 80upx;
		height: 100%;

		// background-color: blue;
	}

	.content .topView .topL image {
		width: 80upx;
		height: 80upx;

		border-radius: 40upx;
	}

	.content .topView .topC {
		max-width: 320upx;
		height: auto;

		margin: 5upx 5upx 5upx 10upx;

		// background-color: yellow;

		display: flex;
		flex-flow: row wrap;
		align-content: space-between;

	}

	.content .topView .topC .title {
		width: 100%;
		height: 50%;

		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;

		font-size: 32upx;

		color: #333;

	}

	.content .topView .topC .status {
		width: 100%;

		// background-color: red;

		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;

		font-size: 27upx;

		color: #333;

	}

	.content .topView .topR {
		height: 100%;

		flex: 1;
		display: flex;
		align-items: center;
		flex-flow: row-reverse;

		// background-color: green;

	}

	.content .topView .attention {
		height: 60upx;
		line-height: 60upx;
		width: 110upx;

		text-align: center;

		font-size: 27upx;

		background-color: #13b6ff;

		border-radius: 30upx;

		color: #fff;



	}

	.content .courseVideo {
		width: 100%;

		background-color: #fff;
		box-sizing: border-box;

		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
	}

	.content .courseVideo .videoView {
		margin: 15upx;
		width: 100%;
		height: 300upx;
		box-sizing: border-box;

		background-color: #fff;

		display: flex;
	}

	.content .courseVideo .videoView .video-container {

		width: 100%;
		margin-left: 15upx;
		margin-right: 15upx;
		height: 100%;
		display: flex;

	}
	.content .courseVideo .videoView .video-container>image{
		width: 100%;
		height: 100%;
	}

	.content .selectItem {
		width: 100%;
		height: 100upx;

		background-color: #fff;
		display: flex;
		flex-direction: column;
		
	}

	.content .selectItem .scrollview {
		width: 100%;
		height: 100upx;
		background-color: #fff;
		border-bottom: 1upx #f2f2f2 solid;
		z-index: 100;

		// background-color: blue;
		// white-space: nowrap;

	}

	.content .selectItem .scrollview .line {
		background-color: #f74163;

		height: 10upx;

		border-radius: 5upx;

		position: absolute;
		bottom: 0upx;

		transition: .5s;
	}

	.content .selectItem .scrollview .items {
		height: 100%;
		line-height: 100upx;

		margin-left: 40upx;
		padding: 0 20upx;

		display: inline-block;
		// background-color: green;
	}

	.content .selectItem .scrollview .items>text {
		// background-color: red;
		font-size: 32upx;
	}

	.content .selectItem .scrollview .items .selected {
		color: #13b6ff;
		font-weight: bold;
	}

	.content .itemAll .swiper {
		height: calc(100vh - 100upx);
		// background-color: red;
	}

	.content .itemAll .swiper swiper-item .swiper-item1 .one {
		// margin: 15upx;
		margin: 0upx;
	}

	.content .itemAll .swiper swiper-item .swiper-item1 .one .body {
		width: 100%;
		display: flex;
		flex-direction: column;

	}

	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.course {
		margin-bottom: 15upx;
		width: 100%;
		height: 100upx;
		background-color: #fff;
		padding: 15upx;
	}

	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.course>.title {
		height: 60%;
	}

	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.course>.title>text {
		font-size: 30upx;
		color: #333;
	}

	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.course>.time {
		height: 40%;

	}

	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.course>.time>text {
		font-size: 28upx;
		color: #999;
	}

	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.contentA {
width: 100%;
		height: 100upx;
	
		background-color: #fff;
		display: flex;
		flex-direction: column;
	}
	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.contentA>.scrollviewA {
		width: 100%;
		height: 100%;
	
		// background-color: blue;
		// white-space: nowrap;
	
	}
	
	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.contentA>.scrollviewA .lineA {
		background-color: #f74163;
	
		height: 10upx;
	
		border-radius: 5upx;
	
		position: absolute;
		bottom: 0upx;
	
		transition: .5s;
	}
	
	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.contentA>.scrollviewA .itemsA {
		height: 100%;
		line-height: 100upx;
	
		margin-left: 40upx;
		padding: 0 20upx;
	
		display: inline-block;
		// background-color: green;
	}
	
	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.contentA>.scrollviewA .itemsA>text {
		// background-color: red;
		font-size: 30upx;
	}
	
	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.contentA>.scrollviewA .itemsA>.selected {
		color: #13b6ff;
		font-weight: bold;
	}
	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.itemAllA .swiper {
		height: calc(100vh - 100upx);
		// background-color: red;
	}
	
	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.itemAllA .swiper swiper-item .swiper-item1 .one {
		margin: 15upx;
	}
	.content .itemAll .swiper swiper-item .swiper-item1 .one .body>.itemAllA .swiper swiper-item .swiper-item1 .two {
		margin: 15upx;
	}
	.content .itemAll .swiper swiper-item .swiper-item2 .two {
		margin: 15upx;
	}

	.content .itemAll .swiper swiper-item .swiper-item3 .three {
		margin: 15upx;
	}

	.content .itemAll .swiper swiper-item .swiper-item4 .four {
		margin: 15upx;
	}

	.botttomView {
		width: 100%;
		// height: 110upx;

		background-color: #ff;

		position: fixed;
		bottom: 0;

		border-top: 1upx #f2f2f2 solid;

		display: flex;
	}
</style>


```




