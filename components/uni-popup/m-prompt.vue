<template>
	<uni-popup ref="popup" @change="onPopChange">
		<view class="box" :style="'width:' + width + 'px;'">
			<text class="title" v-text="title"></text>
			<view class="content">
				<text v-text="content"></text>
			</view>
			<view class="btn-box">
				<view class="cancel" v-text="cancelText" @click="close">
					
				</view>
				<view class="confirm" v-text="confirmText" @click="confirm">
					
				</view>
			</view>
		</view>
	</uni-popup>
</template>

<script>
	import uniPopup from '../uni-popup/uni-popup.vue'
	export default {
		components: {
			uniPopup
		},
		props: {
			title: String,
			content: String,
			cancelText: String,
			confirmText: String
		},
		data() {
			return {
				visible:false,
				width: 0
			}
		},
		methods: {
			open() {
				this.width = window.innerWidth - 75;
				console.log('width', this.width)
				this.visible = true
				this.$refs.popup.open()
			},
			close() {
				this.visible = false
				this.$refs.popup.close()
			},
			confirm() {
				this.$emit('confirm')
				this.close()
			},
			bindChange(e) {
				
			},
			onPopChange({show}) {
				if (!show) {
					this.visible = false
				}
			}
		},
	}
</script>

<style>
	.box {
		display: flex;
		flex-direction: column;
		margin: auto 75rpx;
		height: 434rpx;
		border-radius: 40rpx;
		background-color: white;
	}
	.title {
		margin: 60rpx 40rpx 20rpx 40rpx;
		text-align: center;
		font-size: 40rpx;
		color: #333333;
		font-weight: 600;
	}
	.content {
		display: flex;
		justify-content: center;
		align-items: center;
		text-align: center;
		height: 106rpx;
		margin: 10rpx 40rpx 20rpx 40rpx;
		vertical-align: middle;
		color: #8E8E8E;
		font-size: 28rpx;
	}
	.btn-box {
		display: flex;
		flex-direction: row;
		height: 92rpx;
		width: 100%;
		margin-top: 30rpx;
		margin-bottom: 60rpx;
		justify-content: space-evenly;
	}
	.cancel {
		width: 232rpx;
		height: 92rpx;
		background: #cccccc;
		border-radius: 46rpx;
		text-align: center;
		line-height: 92rpx;
		font-size: 30rpx;
		color: white;
	}
	.confirm {
		width: 232rpx;
		height: 92rpx;
		background-image: url(../../static/img/confirm_btn_bg.png);
		background-repeat: no-repeat;
		background-size: 100% 100%;
		text-align: center;
		line-height: 92rpx;
		font-size: 30rpx;
		color: white;
	}
</style>
