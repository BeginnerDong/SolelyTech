<template>
	<view>
		
		<view class="orderNav d-flex a-center bg-white px-3 py-1 border-bottom">
			<view class="tt d-flex j-center a-center">{{year}}年<image class="arrwB" src="../../static/images/to-promotel-icon.png" mode=""></image></view>
			<view class="tt d-flex j-center a-center">{{month}}月<image class="arrwB" src="../../static/images/to-promotel-icon.png" mode=""></image></view>
		</view>
		<view class="editLine">
			<view class="item d-flex a-center">
				<view class="ll">姓名</view>
				<view class="rr">{{name}}</view>
			</view>
			<view class="item d-flex a-center">
				<view class="ll">职位</view>
				<view class="rr">{{position}}</view>
			</view>
			<view class="item d-flex a-center" v-for="(item,index) in mainData">
				<view class="ll">{{item.description}}</view>
				<view class="rr">{{item.money}}</view>
			</view>
			<!-- <view class="item d-flex a-center">
				<view class="ll">绩效</view>
				<view class="rr">5000.00</view>
			</view>
			<view class="item d-flex a-center">
				<view class="ll">基本薪资</view>
				<view class="rr">7000.00</view>
			</view>
			<view class="item d-flex a-center">
				<view class="ll">奖励金额</view>
				<view class="rr">2366.00</view>
			</view>
			<view class="item d-flex a-center">
				<view class="ll">扣除金额</view>
				<view class="rr">-560.00</view>
			</view>
			<view class="item d-flex a-center">
				<view class="ll">绩效扣除</view>
				<view class="rr">0.00</view>
			</view>
			<view class="item flex">
				<view class="ll">绩效奖励</view>
				<view class="rr">+366.00</view>
			</view> -->
			<view class="item d-flex a-center">
				<view class="ll">总计</view>
				<view class="rr red">{{total}}</view>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:[],
				year:'',
				month:'',
				total:0,
				name:'',
				position:''
			}
		},
		
		onLoad(options) {
			const self = this;
			var date = new Date();
			self.year = date.getFullYear();
			self.month = date.getMonth()+1;
			self.day = date.getDate();
			self.name = uni.getStorageSync('staff_info').info.name;
			self.position = uni.getStorageSync('staff_info').info.passage1;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);	
		},
		
		
		methods: {
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						pagesize: 10,
						is_page: true,
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.searchItem = {
					thirdapp_id: 22,
					relation_user:uni.getStorageSync('staff_info').user_no,
					year:self.year,
					month:self.month-1
				};
				postData.order = {
					money:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
						self.total = 0
						for (var i = 0; i < self.mainData.length; i++) {
							self.total += parseFloat(self.mainData[i].money)
						}
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.salaryFlowGet(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/editInfor.css";
	
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}
	
	.editLine .item{padding: 20rpx 4%;}
	.editLine .item:last-child{border-bottom: 0;}
	.editLine .item:nth-of-type(2n+1){background-color: #fff;}
	.extension{width: 100%;height: 160rpx;padding: 30rpx;box-sizing: border-box;border-radius: 10rpx;background-color: #fff;margin-top: 30rpx;}
	.extension .photo{width: 100rpx;height: 100rpx;border-radius: 50%;margin-right: 20rpx;}
	.ll{width: 50%;}
	.rr{width: 50%;text-align: right;}
</style>
