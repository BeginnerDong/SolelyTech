<template>
	<view>
		
		<view class="mx-2 py-3">
			<view class="font-30 font-weight">起始</view>
			<view class="d-flex a-center mt-20">
				<view class="mr-5 font-26 color6">时间</view>
				<view>{{mainData.start_time>0?Utils.timeto(mainData.start_time*1000,'ymd-hms'):'-------'}}</view>
			</view>
			<view class="d-flex a-center mt-20">
				<view class="mr-5 font-26 color6">缘由</view>
				<view>{{mainData.content}}</view>
			</view>
		</view>
		<view class="f5Bj-H10"></view>
		<view class="mx-2 py-3">
			<view class="font-30 font-weight">到达</view>
			<view class="d-flex a-center mt-20">
				<view class="mr-5 font-26 color6">时间</view>
				<view>{{mainData.arrive_time>0?Utils.timeto(mainData.arrive_time*1000,'ymd-hms'):'-------'}}</view>
			</view>
			<view class="d-flex a-center picLis">
				<view class="tt"><image :src="mainData.mainImg&&mainData.mainImg[0]?mainData.mainImg[0].url:''" mode=""></image></view>
			
			</view>
		</view>
		<view class="f5Bj-H10"></view>
		<view class="mx-2 py-3">
			<view class="font-30 font-weight">返程</view>
			<view class="d-flex a-center mt-20">
				<view class="mr-5 font-26 color6">时间</view>
				<view>{{mainData.back_time>0?Utils.timeto(mainData.back_time*1000,'ymd-hms'):'-------'}}</view>
			</view>
			
		</view>
		<view class="f5Bj-H10"></view>
		<view class="mx-2 py-3">
			<view class="font-30 font-weight">结束</view>
			<view class="d-flex a-center mt-20">
				<view class="mr-5 font-26 color6">时间</view>
				<view>{{mainData.end_time>0?Utils.timeto(mainData.end_time*1000,'ymd-hms'):'-------'}}</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				is_show: false,
				wx_info:{},
				caseData:3,
				mainData:{}
			}
		},
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.searchItem = {
					thirdapp_id: 22,
					type:3,
					id:self.id
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						//self.mainData.behavior = self.array[self.mainData.behavior];
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.routineGet(postData, callback);
			},
		}
	};
</script>

<style>
	page{padding-bottom: 60rpx;}
	.picLis{flex-wrap: wrap;}
	.picLis .tt{width: 300rpx;height: 200rpx;margin:20rpx 30rpx 0 0;}
	
	
</style>