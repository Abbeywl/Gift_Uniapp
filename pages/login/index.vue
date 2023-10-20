<template>
	<view class="wrap">
		<view class="login_box">
			<u-icon name="zhongguojie" custom-prefix="custom-icon" size="300" color=" #e5e5e5"></u-icon>
			<u-form :model="form" ref="uForm">
				<u-form-item class="ipt" prop="name" :border-bottom='false'>
					<u-input v-model="form.name" :border="true" type="number" placeholder='请输入手机号码' />
				</u-form-item>
				<u-form-item class="ipt" prop="password" :border-bottom='false' v-show="!phoneLogin">
					<u-input v-model="form.password" :border="true" placeholder='请输入密码' />
				</u-form-item>
				<u-form-item prop="code" class="ipt" :border-bottom='false' v-show="phoneLogin">
					<u-input placeholder="请输入验证码" :border="true" v-model="form.code" type="number"></u-input>
					<u-button slot="right" size="mini" @click="getCode" ripple-bg-color="#909399">{{codeTips}}
					</u-button>
				</u-form-item>
				<u-verification-code seconds="60" ref="uCode" @change="codeChange"></u-verification-code>
			</u-form>
			<view @click="codeLogin">{{text}}</view>
			<view class="btn">
				<u-button @click="submit" size="medium" :ripple="true" ripple-bg-color="#909399">
					登&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 录</u-button>
			</view>

		</view>

		<!-- <view class="buttom">
			<view class="loginType">
				<view class="wechat item">
					<view class="icon">
						<u-icon size="70" name="weixin-fill" color="rgb(83,194,64)"></u-icon>
					</view>
					微信
				</view>
				<view class="QQ item">
					<view class="icon">
						<u-icon size="70" name="qq-fill" color="rgb(17,183,233)"></u-icon>
					</view>
					QQ
				</view>
			</view>
		</view> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				text: '验证码登录',
				phoneLogin: false,
				codeTips: '获取验证码',
				form: {
					name: '',
					password: '',
					code: null,
				},
				rules: {
					name: [{
						required: true,
						message: '请输入手机号',
						trigger: ['blur', 'change']
					}],
					password: [{
						required: true,
						message: '请输入密码',
						trigger: ['blur', 'change']
					}],
					code: [{
						required: true,
						message: '请输入验证码',
						trigger: ['change', 'blur'],
					}, ],
				}
			}
		},
		onReady() {
			this.$refs.uForm.setRules(this.rules);
		},
		computed: {
			inputStyle() {
				let style = {};
				if (this.tel) {
					style.color = "#fff";
					style.backgroundColor = this.$u.color['warning'];
				}
				return style;
			}
		},
		methods: {
			submit() {
				if (this.form.name != "") {
					if ((this.phoneLogin && this.form.code || !this.phoneLogin && this.form.password)) {
						// this.$u.route({
						// 	url: 'pages/main/index'
						// })
						uni.reLaunch({
							url: '/pages/main/index'
						})
						console.log(1)
					}
				}


				// this.$refs.uForm.validate(valid => {
				// 	if (valid) {
				// 		console.log('验证通过');

				// 	} else {
				// 		console.log('验证失败');
				// 	}
				// });

			},
			// 获取验证码
			getCode() {
				if (this.$refs.uCode.canGetCode) {
					// 模拟向后端请求验证码
					uni.showLoading({
						title: '正在获取验证码',
						mask: true
					})
					setTimeout(() => {
						uni.hideLoading();
						// 这里此提示会被this.start()方法中的提示覆盖
						this.$u.toast('验证码已发送');

						// 通知验证码组件内部开始倒计时
						this.$refs.uCode.start();
					}, 2000);
				} else {
					this.$u.toast('倒计时结束后再发送');
				}
			},
			codeChange(text) {
				this.codeTips = text;
			},
			codeLogin() {
				this.text = '密码登录'
				this.phoneLogin = !this.phoneLogin
			}
		}
	};
</script>

<style lang="scss" scoped>
	.wrap {
		background: url(../../static/bg.jpg) no-repeat fixed center;
		font-size: 28rpx;
		width: 100vw;
		height: 100vh;
		overflow: hidden;

		.login_box {

			width: 100%;

			& /deep/ uni-view,
			& /deep/ input {
				color: #e5e5e5;
			}

			& /deep/ uni-button {
				background-color: #e5e5e5;

			}

			margin-top: 36%;
			display: flex;
			justify-content: center;
			align-items: center;
			flex-wrap: wrap;

			& /deep/ .u-form {
				display: flex;
				justify-content: center;
				align-items: center;
				flex-wrap: wrap;
			}

			& /deep/ .custom-icon-marketing {
				padding: 30rpx 0;
			}

			.btn {
				margin-top: 30rpx;
				width: 100%;
				text-align: center;
			}

			.ipt {
				width: 500rpx;
				display: block;
				margin-top: 20rpx;
			}
		}

	}
</style>
