<template>
	<view>
		<uni-list :border="true">
			<!-- 自定义右侧内容 -->
			<uni-list-chat title="小明结婚" :avatar-circle="true" avatar="../../static/marry.png" note="霍山酒店办的酒席"
				time="2020-02-02 20:20" badge-positon="left" to="../main/indexList">
				<view class="chat-custom-right">
					<view class="money">82,700 元</view>
					<view class="chat-custom-text">2023-01-23</view>
				</view>
			</uni-list-chat>
			<uni-list-chat title="霍山新房乔迁" :avatar-circle="true" avatar="../../static/home_get.png"
				to="../main/indexList" note="霍山酒店办的酒席" time="2020-02-02 20:20" badge-positon="left">
				<view class="chat-custom-right">
					<view class="money">82,700 元</view>
					<view class="chat-custom-text">2023-01-23</view>
				</view>
			</uni-list-chat>
			<uni-list-chat title="张大爷60大寿" :avatar-circle="true" avatar="../../static/cake.png" to="../main/indexList"
				note="霍山酒店办的酒席" time="2020-02-02 20:20" badge-positon="left">
				<view class="chat-custom-right">
					<view class="money">6,700 元</view>
					<view class="chat-custom-text">2009-01-23</view>
				</view>
			</uni-list-chat>
			<uni-list-chat title="李某的升学酒" :avatar-circle="true" avatar="../../static/student.png" to="../main/indexList"
				note="霍山酒店办的酒席" time="2020-02-02 20:20" badge-positon="left">
				<view class="chat-custom-right">
					<view class="money">6,700 元</view>
					<view class="chat-custom-text">2009-01-23</view>
				</view>
			</uni-list-chat>
			<uni-list-chat title="李某的丧事" :avatar-circle="true" 
				avatar="../../static/graveyard.png" to="../main/indexList" note="霍山酒店办的酒席" time="2020-02-02 20:20"
				badge-positon="left">
				<view class="chat-custom-right">
					<view class="money">6,700 元</view>
					<view class="chat-custom-text">2009-01-23</view>
				</view>
			</uni-list-chat>

		</uni-list>
		<view class="u-add-btn" @click="addFn">
			<u-icon name="plus"></u-icon>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				avatar: ""
			};
		},
		methods: {
			addFn(){
				uni.navigateTo({
					url: './addBook'
				})
			}
		}
	}
</script>

<style lang="scss">
	.chat-custom-text {
		font-size: 12rpx;
		color: #999;
		text-align: right;
	}

	.money {
		font-size: 36rpx;
		color: #aa0000;
		text-align: right;
	}

	.u-add-btn {
		text-align: center;
		line-height: 100rpx;
		font-size: 45rpx;
		border-radius: 50%;
		color: #333;
		width: 100rpx;
		height: 100rpx;
		border: 1px solid #333;
		background-color: rgba($color: #fff, $alpha: 0.7);
		position: fixed;
		right: 5%;
		bottom: 15%;
	}
</style>
