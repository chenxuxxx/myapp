<template>
	<view class="content">
		<!-- <image class="logo" src="/static/logo.png"></image> -->
		<view class="text-area">
			<input v-model="phone" placeholder="请输入电话号码" class="inputText" type="number"/>
			<button type="primary" @click="callPhone">拨打</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				phone: ''
			}
		},
		onLoad() {

		},
		methods: {
			callPhone() {
				uni.makePhoneCall({
				    phoneNumber: this.phone+'' //仅为示例
				});
			}
		}
	}
</script>

<style lang="scss">
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		.text-area {
			position: absolute;
			top: 50%;
			transform: translateY(-50%);
			.inputText {
				height: 80rpx;
				line-height: 80rpx;
				background-color: #eee;
			}
		}
	}

</style>
