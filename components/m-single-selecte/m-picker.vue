<template>
	<uni-popup ref="popup" type="bottom" @change="onPopChange">
		<view class="select-box">
			<view class="hardline">
				<text class="picker-action" @click="close" v-text="cancelText"></text>
				<text class="title" v-text="title"></text>
				<text class="picker-action" @click="confirm" v-text="confirmText"></text>
			</view>
			<picker-view v-if="visible" class="picker-view" :value="value" @change="bindChange">
				<picker-view-column v-for="(empty, i) in columns" :key="i">
					<view class="item" v-for="(item,index) in lists[i]" :key="index" v-text="item[keys[i]]"></view>
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
			title:{
				type: String,
				default: ''
			},
			lists: {
				type: Array,
				default: []
			},
			cancelText: {
				type: String,
				default: '取消'
			},
			confirmText: {
				type: String,
				default: '确认'
			},
			keys: {
				type: Array,
				default: ['text']
			}
		},
		data() {
			return {
				columns: [],
				selectIndex: 0,
				selectInd: 0,
				visible:false,
				key: '',
				value: [],
				subLists: []
			}
		},
		created() {
			let column = 1
			if (column != this.lists.length) {
				column = this.lists.length
			}
			if (column > 3) {
				column = 3
			}
			for (let i = 0; i < column; i ++) {
				this.columns.push('')
			}
		},
		methods: {
			open(key) {
				console.log(this.lists)
				this.selectIndex = 0
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
