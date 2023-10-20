<template>
	<view class="main">
		<u-form :model="form" ref="uForm" :rules="rules" error-type="border-bottom">
			<u-form-item label="姓名"prop="name" >
				<u-input v-model="form.name" placeholder="请输入姓名"/>
			</u-form-item>
			<u-form-item label="礼金" prop="amount" >
				<u-input v-model="form.amount" type="number" @input="inputAmount(form.amount)" placeholder="请输入礼金" />
			</u-form-item>
			<u-form-item label="  ">
				<u-input :disabled="true" placeholder="大写金额" />
			</u-form-item>
			<u-form-item label="关系" prop="relation">
				<u-input v-model="form.relation" placeholder="请输入与户主关系" />
			</u-form-item>
			<u-form-item label="备注"prop="note">
				<u-input v-model="form.note"  type="textarea" placeholder="请输入备注" />
			</u-form-item>
			<u-form-item label="" prop="radio" >
				<u-radio-group v-model="form.radio">
					<u-radio v-for="(item, index) in radioList" :key="index" :name="item.name"
						:disabled="item.disabled">
						{{ item.name }}
					</u-radio>
				</u-radio-group>
			</u-form-item>
		</u-form>
		<u-button @click="submit"type="success"  size="medium" class="btn">提交</u-button>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				dis: true,
				form: {
					amount: 0,
					name: '',
					note: '',
					relation: '',
					radio: false,
				},
				rules: {
					name: [{
						required: true,
						message: '请输入姓名',
						trigger: ['blur', 'change']
					}],
					amount: [{
						required: true,
						message: '请输入礼金',
						trigger: ['blur', 'change']
					}],
					note: [{
						required: true,
						message: '请输入礼金',
						trigger: ['blur', 'change']
					}],
					relation: [{
						required: true,
						message: '请输入礼金',
						trigger: ['blur', 'change']
					}],
					radio: [{
						required: true,
						message: '请输入礼金',
						trigger: ['blur', 'change']
					}]
				},
				radioList: [{
						name: '嫁娶',
						disabled: false
					},
					{
						name: '升学',
						disabled: false
					},
					{
						name: '生日宴',
						disabled: false
					},
					{
						name: '乔迁',
						disabled: false
					},
					{
						name: '丧事',
						disabled: false
					}
				],
			};
		},
		// 必须要在onReady生命周期，因为onLoad生命周期组件可能尚未创建完毕
		onReady() {
			this.$refs.uForm.setRules(this.rules);
		},
		methods: {
			submit() {
				this.$refs.uForm.validate(valid => {
					if (valid) {
						console.log('验证通过');
					} else {
						console.log('验证失败');
					}
				});
			},
			inputAmount(number) {
				let ret = ''
				if (number !== '' && number != null && number !== '0') {
					let unit = '仟佰拾亿仟佰拾万仟佰拾元角分'
					let str = ''
					number += '00'
					const point = number.indexOf('.')
					if (point >= 0) {
						number = number.substring(0, point) + number.substr(point + 1, 2)
					}
					unit = unit.substr(unit.length - number.length)
					for (let i = 0; i < number.length; i++) {
						str += '零壹贰叁肆伍陆柒捌玖'.charAt(number.charAt(i)) + unit.charAt(i)
					}
					ret =
						str
						.replace(/零(仟|佰|拾|角)/g, '零')
						.replace(/(零)+/g, '零')
						.replace(/零(万|亿|元)/g, '$1')
						.replace(/(亿)万|(拾)/g, '$1$2')
						.replace(/^元零?|零分/g, '')
						.replace(/元$/g, '元') + '整'
				}
				this.form.text = ret
			},
		}
	};
</script>
<style scoped lang="scss">
	.main {
		padding: 0 40rpx;
		margin: 0 auto;
		text-align: center;
		.btn{
			margin-top: 100rpx;
		}
	}
	
</style>
