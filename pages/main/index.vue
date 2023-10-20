<template>
	<view class="wrap">
		<u-row gutter="16">
			<u-col span="16" class="t">
				<u-icon name="zb" custom-prefix="custom-icon" size="50" color=" #2979ff"></u-icon>
				<text class="title">账簿类型</text>
			</u-col>
		</u-row>
		<u-row gutter="16">
			<u-col span="4" class="text_center  ">
				<view class="_iconBox ">
					<u-icon name="jiehun" custom-prefix="custom-icon" size="75" color=" #8a8a8a"></u-icon>
				</view>
				<view class="text_center">婚 宴</view>
			</u-col>
			<u-col span="4" class="text_center">
				<view class="_iconBox ">
					<u-icon name="xinfang" custom-prefix="custom-icon" size="75" color=" #8a8a8a"></u-icon>
				</view>
				<view class="text_center">乔 迁</view>
			</u-col>
			<u-col span="4" class="text_center">
				<view class="_iconBox ">
					<u-icon name="bojuelvpaiicontilian_huabanfuben" custom-prefix="custom-icon" size="75" color=" #8a8a8a"></u-icon>
				</view>
				<view class="text_center">生日宴</view>
			</u-col>
			<u-col span="4" class="text_center">
				<view class="_iconBox ">
					<u-icon name="shuyi_xuesheng" custom-prefix="custom-icon" size="75" color=" #8a8a8a"></u-icon>
				</view>
				<view class="text_center">升学宴</view>
			</u-col>
			<u-col span="4" class="text_center">
				<view class="_iconBox ">
					<u-icon name="siwangbinzang" custom-prefix="custom-icon" size="75" color=" #8a8a8a"></u-icon>
				</view>
				<view class="text_center">丧 事</view>
			</u-col>
			
		</u-row>
		<u-gap height="80" bg-color="#ffffff"></u-gap>
		<u-row gutter="16">
			<u-col span="16" class="t">
				<u-icon name="new" custom-prefix="custom-icon" size="40" color=" #aa0000"></u-icon>
				<text class="title">最新账单</text>
			</u-col>
		</u-row>
		<u-row gutter="0">
			
		<view class="uni-list">
					<view class="uni-list-cell">
						<view class="uni-list-cell-left">
							当前选择
						</view>
						<view class="uni-list-cell-db">
							<picker mode="date" value="month" fields='mouth' @change="bindTimeChange">
								<view class="uni-input">{{time}}</view>
							</picker>
						</view>
					</view>
				</view>
		</u-row>
	</view>
</template>

<script>
	export default {
		data() {
			  const currentDate = this.getDate({
			            format: true
			        })
			return {
				  time: currentDate
			}
		},
		methods: {
			
			   bindTimeChange: function(e) {
			            this.time = e.detail.value
			        },
					    getDate(type) {
					            const date = new Date();
					            let year = date.getFullYear();
					            let month = date.getMonth() + 1;
					            let day = date.getDate();
					
					            if (type === 'start') {
					                year = year - 60;
					            } else if (type === 'end') {
					                year = year + 2;
					            }
					            month = month > 9 ? month : '0' + month;
					            day = day > 9 ? day : '0' + day;
					            return `${year}-${month}-${day}`;
					        }
		}
	}
</script>
<style scoped lang="scss">
	._iconBox{
		width: 150rpx;
		height: 150rpx;
		border-radius: 50%;
		text-align: center;
		margin: 0 auto;
		display: flex;
		justify-content: center;
		align-items: center;
		align-content: center;
		margin: 0 auto;
		border: 1px solid #D8D8D8;
	}
	.title {
		color: $u-main-color;
		padding-left: 15rpx;
	}

	.wrap {
		padding: 24rpx;
		color: $u-main-color;
		line-height: 60rpx;

		.t {
			align-items: center;
			display: flex;
		}
	}
	.text_center{
		text-align: center;
	}
.margin_auto{
	margin:  0 auto;

}
	
	.space_between {
		display: flex;
		justify-content: space-between;
	}
</style>
