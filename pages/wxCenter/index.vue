<template>
	<view>
		<u-navbar :is-back="false" title="　" :border-bottom="false">
			<view class="u-flex u-row-right" style="width: 100%;" @click="photo">
				<view class="camera u-flex u-row-center">
					<u-icon name="camera-fill" color="#000000" size="48"></u-icon>
				</view>
			</view>
		</u-navbar>
		<view class="u-flex user-box u-p-l-30 u-p-r-20 u-p-b-30">
			<view class="u-m-r-10">
				<u-avatar :src="pic" size="140"></u-avatar>
			</view>
			<view class="u-flex-1">
				<view class="u-font-18 u-p-b-20">uView ui</view>
				<view class="u-font-14 u-tips-color">微信号:helang_uView</view>
			</view>
			<view class="u-m-l-10 u-p-10" @click="shaoMa">
				<u-icon name="scan" color="#969799" size="28"></u-icon>
			</view>
			<view class="u-m-l-10 u-p-10">
				<u-icon name="arrow-right" color="#969799" size="28"></u-icon>
			</view>
		</view>
		
		<view class="u-m-t-20">
			<u-cell-group>
				<u-cell-item icon="rmb-circle" title="支付"></u-cell-item>
			</u-cell-group>
		</view>
		
		<view class="u-m-t-20">
			<u-cell-group>
				<u-cell-item icon="star" title="收藏"></u-cell-item>
				<u-cell-item icon="photo" title="相册"></u-cell-item>
				<u-cell-item icon="coupon" title="卡券"></u-cell-item>
				<u-cell-item icon="heart" title="关注"></u-cell-item>
			</u-cell-group>
		</view>
		
		<view class="u-m-t-20">
			<u-cell-group>
				<u-cell-item icon="setting" title="设置"></u-cell-item>
			</u-cell-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				pic:'https://uviewui.com/common/logo.png',
				show:true
			}
		},
		onLoad() {
			
		},
		methods: {
			shaoMa() {
				uni.scanCode({
					success: function (res) {
							console.log('条码类型：' + res.scanType);
							console.log('条码内容：' + res.result);
					}
				});
			},
			photo() {
				uni.chooseImage({
				count: 6,
				sizeType: ['original', 'compressed'],
				// sourceType: ['album'],
				success: function(res) {
						// 预览图片
						uni.previewImage({
								urls: res.tempFilePaths,
								longPressActions: {
										itemList: ['发送给朋友', '保存图片', '收藏'],
										success: function(data) {
												console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
										},
										fail: function(err) {
												console.log(err.errMsg);
										}
								}
						});
				}
				});
			}
		}
	}
</script>

<style lang="scss">
page{
	background-color: #ededed;
}

.camera{
	width: 54px;
	height: 44px;
	
	&:active{
		background-color: #ededed;
	}
}
.user-box{
	background-color: #fff;
}
</style>
