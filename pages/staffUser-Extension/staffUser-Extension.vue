<template>
	<view>
		
		<view class="orderNav d-flex a-center bg-white py-3">
			<view class="tt d-flex a-center j-center">起始时间<image class="arrwB" src="../../static/images/to-promotel-icon.png" mode=""></image></view>
			<view class="tt d-flex a-center j-center">截止时间<image class="arrwB" src="../../static/images/to-promotel-icon.png" mode=""></image></view>
		</view>
		<view class="mx-2">
			<view class="extension d-flex a-center" v-for="(item,index) in extensionData" :key="index">
				<view class="photo"><image src="../../static/images/to-promotel-img.png" mode=""></image></view>
				<view>
					<view>涸鲋得水</view>
					<view class="mt-1 font-26 color6">2020-04-15</view>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				score:'',
				wx_info:{},
				extensionData:3
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {

		},
	};
</script>

<style>
	@import "../../assets/style/orderNav.css";
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}
	
	.extension{width: 100%;height: 160rpx;padding: 30rpx;box-sizing: border-box;border-radius: 10rpx;background-color: #fff;margin-top: 30rpx;}
	.extension .photo{width: 100rpx;height: 100rpx;border-radius: 50%;margin-right: 20rpx;}
</style>
