<template>
	<view>
		<view id="topView" class="topView position">
			<view class="back" @click="backBtn">
				<span><-</span>
			</view>
			<view class="navc">
				<view class="item">
					<text>首页</text>
				</view>
				<view class="item">
					<text>升级会员</text>
				</view>
				<view class="item">
					<text>推广</text>
				</view>
				<view class="item">
					<text>关注</text>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		name: 'navc',
		data() {
			return {

			};
		},
		methods: {
			//返回按钮
			backBtn() {
				uni.navigateBack({
					delta: 1,
				});
			},
		}
	}
</script>

<style lang="scss">
	page {
		position: relative;

	}

	.topView {
		width: 100%;
		height: 90upx;

		background-color: #f2f2f2;

		position: fixed;
		top: 0upx;
		z-index: 3;

		display: flex;
	}

	.topView .back {
		width: 100upx;
		height: 100%;

		// background-color: red;

		display: flex;
		justify-content: center;
		align-items: center;
	}

	.topView .back span {
		font-size: 40upx;
	}

	.topView .navc {
		flex: 1;
		height: 100%;

		// background-color: yellow;

		display: flex;
		flex-direction: row-reverse;
		align-items: center;

		overflow: hidden;
	}

	.topView .navc .item {
		min-width: 10%;
		height: 40%;

		// background-color: red;

		border-left: 4upx #e5e5e5 solid;

		display: flex;
		justify-content: center;
		align-items: center;
	}

	.topView .navc .item:last-child {
		border-left: none;
	}

	.topView .navc .item text {
		font-size: 35upx;

		color: #333;

		margin: 0 15upx;
	}
</style>
