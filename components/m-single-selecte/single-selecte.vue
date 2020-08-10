<template>
	<uni-popup ref="popup" type="bottom" @change="onPopChange">
		<view class="select-box">
			<view class="hardline">
				<text class="picker-action" @click="close">取消</text>
				<text class="title" v-text="title"></text>
				<text class="picker-action" @click="confirm">确定</text>
			</view>
			<picker-view v-if="visible" class="picker-view" :value="value" @change="bindChange">
				<picker-view-column>
					<view class="item" v-for="(item,index) in lists" :key="index" v-text="item.text"></view>
				</picker-view-column>
				<picker-view-column v-if="column == 2">
					<view class="item" v-for="(item,index) in subLists" :key="index + 10" v-text="item.product"></view>
				</picker-view-column>
			</picker-view>
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
			column: {
				type: Number,
				default: 1
			},
			title:{
				type: String,
				default: ''
			},
			lists: {
				type: Array,
				default: []
			},
			// subLists: {
			// 	type: Array,
			// 	default: []
			// },
			selectType: {
				type: Number,
				default: 0
			}
		},
		data() {
			return {
				selectIndex: 0,
				selectInd: 0,
				visible:false,
				key: '',
				value: [],
				subLists: []
			}
		},
		methods: {
			open(key) {
				this.selectIndex = 0
				if (this.column == 2) {
					this.subLists = this.lists[0].productList
				}
				this.visible = true
				this.key = key
				this.$refs.popup.open()
			},
			close() {
				this.visible = false
				this.$refs.popup.close()
			},
			confirm() {
				this.$emit('change', this.selectIndex, this.selectInd)
				this.close()
			},
			bindChange(e) {
				console.log(e.target.value)
				let index = e.target.value[0];
				this.selectIndex = index;
				if (this.column == 2) {
					this.subLists = this.lists[index].productList
					this.selectInd = e.target.value.length == 2 ? e.target.value[1] : 0
				}
				// this.selected = this.lists[index].city;
			},
			onPopChange({show}) {
				if (!show) {
					this.visible = false
				}
			}
		}
	}
</script>

<style>
	.select-box {
		display: flex;
		flex-direction: column;
		width: 100%;
		height: 567rpx;
		background-color: white;
		border-top-left-radius: 30rpx;
		border-top-right-radius: 30rpx;
	}
	.hardline {
		display: flex;
		flex-direction: row;
		align-items: center;
		height: 93rpx;
		width: 100%;
		align-self: center;
		border-bottom: 1rpx solid #DDE3EC;
	}
	.picker-view {
		width: 100%;
		flex: 1;
		background-color: white;
	}
	.picker-action:nth-child(1) {
		color: #999999;
		margin-left: 34rpx;
	}
	.picker-action {
		font-size: 28rpx;
	}
	.picker-action:nth-last-child(1) {
		margin-right: 34rpx;
		color: #FF7D1C;
	}
	.title {
		color: #333333;
		font-size: 32rpx;
		flex: 1;
		text-align: center;
	}
	.item {
		text-align: center;
	}
</style>
