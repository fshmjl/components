<template>
	<view class="row">
		<view class="head" v-text="head" :style="headStyle"></view>
		<view class="content" v-text="content" :style="contentStyle"></view>
	</view>
</template>

<script>
	export default {
		props: {
			head: {
				type: String,
				default: ''
			},
			width: {
				type: String,
				default: '140rpx' 
			},
			maxWidth: {
				type: String,
				default: '200rpx' 
			},
			headColor: {
				type: String,
				default: '#999999'
			},
			headFontSize: {
				type: String,
				default: '28rpx'
			},
			contentColor: {
				type: String,
				default: '#333333'
			},
			contentFontSize: {
				type: String,
				default: '28rpx'
			},
			content: String,
			contentLeft: {
				type: String,
				default: '16rpx'
			},
			height: {
				type: String,
				default: '40rpx'
			}
		},
		data() {
			return {
				contentWidth: '100%',
				headStyle: {
					'max-width': this.maxWidth,
					width: this.width,
					color: this.headColor,
					'font-size':this.headFontSize,
				},
				contentStyle: {
					color: this.contentColor,
					'font-size':this.contentFontSize,
					'margin-left': this.contentLeft,
					width: this.contentWidth,
					height: this.height,
					'margin-bottom': this.height == '40rpx' ? '0rpx' : '10rpx',
					'line-height': this.height == '40rpx' ? '40rpx' : 'auto',
					'white-space': this.height == '40rpx' ? 'nowrap' : 'break-spaces',
					'text-overflow': this.height == '40rpx' ? 'ellipsis' : 'clip',
					'overflow': this.height == '40rpx' ? 'hidden' : 'auto',
				}
			};
		},
		created() {
			let width = window.innerWidth - 34 - 24 - parseFloat(this.contentLeft)/2 - parseFloat(this.width)/2
			this.contentStyle.width = width + 'px'
		}
	}
</script>

<style>
	.row {
		display: flex;
		flex-direction: row;
		height: auto;
	}
	.head {
		margin-left: 20rpx;
		margin-top: 10rpx;
		height: 40rpx;
		margin-bottom: 10rpx;
	}
	.content {
		margin-top: 10rpx;
		line-height: 40rpx;
		margin-right: 20rpx;
		white-space:nowrap;
		text-overflow:ellipsis; 
		overflow:hidden;
	}
</style>
