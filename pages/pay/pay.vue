<template>
	<view>
		 
		<view class="w-600 m-a">
				<view class="font-40 my10">请输入支付金额</view>
				<input placeholder="请输入支付金额" v-model="price" type="digit" style="border: 1px solid #e5e5e5;
		height: 100rpx;
		line-height: 100rpx;
		margin-bottom: 50rpx;
		text-align: center;
		border-radius: 20rpx;"/>
				<view class="wh600 Mgb colorf text-c font-32 radius40 py-2" @click="submit">确定</view>
			
				<!-- <view class="gz py-5 radius10 font-26 letter1 mt-3 colorf text-c" v-if="is_show" @click="Router.navigateTo({route:{path:'/pages/meal-ji/meal-ji'}})">激活成功！</view> -->
				<!-- <view class="gz py-5 radius10 font-26 letter1 mt-3 colorf text-c" v-if="is_show" >激活失败！</view> -->
			</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				price:''
			}
		},
		
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				if(self.price==''){
					self.$Utils.showToast('请输入金额', 'none')
					return
				};
				self.pay = {
					wxPay:{
						price:self.price,
						trade_type:'JSAPI'
					}
				};

				
				self.addOrder()
				
			},
			
			
			
			addOrder() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						self.goPay()
			
					} else {
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};
				};
				self.$apis.addVirtualOrder(postData, callback);
			},
			
			goPay() {
				const self = this;
				const postData = self.$Utils.cloneForm(self.pay);
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
				};
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									self.$Utils.showToast('支付成功', 'none')
									setTimeout(function() {
										uni.navigateBack({
											delta:1
										})
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
									self.$Utils.showToast('支付失败', 'none')
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							self.$Utils.showToast('支付成功', 'none')
							setTimeout(function() {
								uni.navigateBack({
									delta:1
								})
							}, 1000);
						};
					} else {
						uni.setStorageSync('canClick', true);
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};
				};
				self.$apis.pay(postData, callback);
			},
		
		}
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	page{padding-bottom: 60rpx;}
	
	textarea{border: 0;height: 400rpx;font-size: 28rpx;}
	.w-600{width: 600rpx;}
	.m-a{margin: auto;}
	.my10{margin: 100rpx 0;}
	.Mgb{background-color: #11a52c;}
	.text-c{ text-align: center; }
	.colorf{color:#fff}
	.radius40{border-radius: 40rpx;}
	.py-2 { padding-top: 20rpx;padding-bottom: 20rpx;}
</style>
