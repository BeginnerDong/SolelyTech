<template>
	<view>
		<view v-for="(item,index) in mainData.log" :key="index">
			<view class="mx-2 py-3">
				<view class="font-30 font-weight" v-if="item.behavior==1">起始</view>
				<view class="font-30 font-weight" v-if="item.behavior==2">到达</view>
				<view class="font-30 font-weight" v-if="item.behavior==3">返程</view>
				<view class="font-30 font-weight" v-if="item.behavior==4">结束</view>
				<view class="d-flex a-center mt-20">
					<view class="mr-5 font-26 color6">时间</view>
					<view>{{item.create_time}}</view>
				</view>
				<map style="width: 100%; height: 200px;" :latitude="item.latitude" :longitude="item.longitude" :markers="item.covers">
				</map>
				<!-- <view class="d-flex a-center mt-20">
					<view class="mr-5 font-26 color6">缘由</view>
					<view>{{mainData.content}}</view>
				</view> -->
			</view>
			<view class="f5Bj-H10"></view>
		</view>
		
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
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
				postData.getAfter = {
					log:{
						tableName:'Log',
						middleKey:'id',
						key:'relation_id',
						condition:'=',
						searchItem:{
							status:1,
							relation_table:'Routine'
						},
						order:{
							create_time:'asc'
						}
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						//self.mainData.behavior = self.array[self.mainData.behavior];
						for (var i = 0; i < self.mainData.log.length; i++) {
							self.mainData.log[i].covers = [{
								latitude: self.mainData.log[i].latitude,
								longitude: self.mainData.log[i].longitude,
								iconPath: '../../static/images/contact-usl-icon2.png'
							}]
						};
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