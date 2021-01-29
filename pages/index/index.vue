<template>
	<view class="content">
		<!-- <image class="logo" src="/static/logo.png"></image> -->
		<view class="text-area">
			<input v-model="phone" placeholder="请输入电话号码" class="inputText" type="number"/>
			<button type="primary" @click="callPhone">拨打</button>
			<view>
        <button @tap="startRecord">开始录音</button>
        <button @tap="endRecord">停止录音</button>
        <button @tap="playVoice">播放录音</button>
    	</view>
		</view>
	</view>
</template>

<script>
const recorderManager = uni.getRecorderManager();
const innerAudioContext = uni.createInnerAudioContext();
innerAudioContext.autoplay = true;
	export default {
		data() {
			return {
				title: 'Hello',
				phone: '',
				voicePath: ''
			}
		},
		onLoad() {
			let self = this;
			recorderManager.onStop(function (res) {
					console.log('recorder stop' + JSON.stringify(res));
					self.voicePath = res.tempFilePath;
			});
    },
		methods: {
			callPhone() {
				uni.makePhoneCall({
				    phoneNumber: this.phone+'' //仅为示例
				});
			},
			startRecord() {
				console.log('开始录音');
				recorderManager.start();
			},
			endRecord() {
					console.log('录音结束');
					recorderManager.stop();
			},
			playVoice() {
					console.log('播放录音');
					if (this.voicePath) {
							innerAudioContext.src = this.voicePath;
							innerAudioContext.play();
					}
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
