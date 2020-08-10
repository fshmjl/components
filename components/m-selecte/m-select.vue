<template>
	<view class="select">
		<text class="item-text" v-text="head"></text>
		<view v-if="hasValue" class="select-box" @click="selectAction()">
			<text class="item-text item-text1" v-text="content"></text>
			<view class="sanjiao"></view>
		</view>
		<view v-else class="select-box">
			<text class="item-text item-text1"></text>
			<view class="sanjiao"></view>
		</view>
		<m-picker ref="picker" :title="head" :lists="[list, list]" :keys="['text','text']"></m-picker>
	</view>
</template>

<script>
	import mPicker from '../m-single-selecte/m-picker.vue'
	export default {
		components: {
			mPicker
		},
		props: {
			head: {
				type: String,
				default: ''
			},
			headWidth: {
				type: String,
				default: '140rpx'
			},
			content: {
				type: String,
				default: ''
			},
			placeholder: {
				type: String,
				default: ''
			},
			list: {
				type: Array,
				default: []
			}
		},
		data() {
			return {
				hasValue: true,
				headStyle: {
					width: this.headWidth
				}
			}
		},
		methods: {
			selectAction() {
				this.$refs.picker.open()
			},
			openPopup() {
				this.$emit('click')
			}
		},
		created() {
			if (this.list.length == 0) {
				this.hasValue = false
			}
		}
	}
</script>

<style>
	.select {
		display: flex;
		flex-direction: row;
		height: 103rpx;
		justify-items: center;
		padding: 0 28rpx;
		background-color: white;
	}

	.item-text,
	.item-text1 {
		color: #333333;
		font-size: 28rpx;
		height: 103rpx;
		line-height: 103rpx;
		font-weight: SC;
	}

	.select-box {
		display: flex;
		flex-direction: row;
		background-color: #F7F9FD;
		margin-left: 23rpx;
		margin-top: 17rpx;
		justify-content: center;
		flex: 1;
		height: 70rpx;
		justify-content: space-between;
		padding-right: 10rpx;
	}

	.item-text1 {
		margin-left: 20rpx;
		line-height: 69rpx;
	}

	.sanjiao {
		width: 0;
		height: 0;
		border-left: 10rpx solid #E4E4E4;
		border-right: 10rpx solid #F7F9FD;
		border-bottom: 10rpx solid #F7F9FD;
		border-top: 10rpx solid #F7F9FD;
		align-self: center;
	}
</style>
