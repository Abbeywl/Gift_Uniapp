<template>
	<u-index-list :scrollTop="scrollTop" :index-list="indexList">
		<view v-for="(item, index) in list" :key="index">
			<u-index-anchor :index="item.letter" />
			<view class="list-cell u-border-bottom " v-for="(item1, index) in item.data" :key="index">
				<view>
					{{item1.name}}
				</view>
				<view>
					100 元
				</view>
			</view>
		</view>
		<view class="list-cell u-border-bottom ">
			<view>
				总计:
			</view>
			<b>
				100 元
			</b>
		</view>
	</u-index-list>
</template>

<script>
	import indexList from "@/common/js/index.list.js";
	const letterArr = indexList.list.map(val => {
		return val.letter;
	})
	export default {
		data() {
			return {
				scrollTop: 0,
				indexList: letterArr,
				list: indexList.list
			}
		},
		onPageScroll(e) {
			this.scrollTop = e.scrollTop;
		}
	}
</script>

<style lang="scss" scoped>
	.list-cell {
		width: 90% !important;
		display: flex;
		box-sizing: border-box;
		justify-content: space-between;
		width: 100%;
		padding: 10px 24rpx;
		overflow: hidden;
		color: $u-content-color;
		font-size: 14px;
		line-height: 24px;
		background-color: #fff;
	}
</style>
